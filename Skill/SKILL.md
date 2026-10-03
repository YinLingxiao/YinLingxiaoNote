---
name: upload-note
description: 把笔记、Obsidian .md 或 Word 转出的 markdown 整理成墨浅笔记站可上传的 page bundle，并按 Site API 规则校验。用户说『做成可上传的笔记文件夹』『准备上传笔记』『整理成 note bundle』『上传到 note』『检查笔记能不能上传』时使用。只处理笔记，不处理博客。
draft: true
---

# 墨浅笔记上传包

产出一个可在 `note.moqian.me/admin/upload`（本地 `http://localhost:3001/admin/upload`）直接选择的文件夹。校验以 `shared/upload/validation.ts`、`Site-api/src/content/policy.ts`、`content-store.ts` 为准。接口 `POST /api/admin/content/note`。

## 先确定

- 分类：上传页单独填写，不由文件夹决定。按课程或主题，如 `高等数学`。
- slug：即文件夹名。

## 文件夹

```text
<slug>/
├─ index.md
└─ figure-1.png   # 可选；所有图片与 index.md 同层
```

违反任一条会被拒：

- 只选一个文件夹，内部不能有子文件夹。
- 恰好一个 `index.md`，不能有其他 `.md`。
- 其余文件只能是 `png` `jpg` `jpeg` `gif` `webp` `avif`，且必须是真实图片。
- slug 匹配 `^[a-z0-9]+(?:-[a-z0-9]+)*$`，长度不超过 80。如 `curve-integral`。
- 文件名长度不超过 120，不能有空格和 `% ? # ( ) [ ]`，不能以 `.` 开头或结尾，不能是 `con`/`nul` 等 Windows 保留名。
- `index.md` 为 UTF-8，非空，无 NUL 字节。
- 默认上限：32 个文件；正文 2 MB；单图 10 MB、4000 万像素；合计 50 MB。
- slug 在 `Notes/` 任意分类下不能已存在，已有内容不会被覆盖。构建期同名会变成 `<分类>--<slug>`，但上传接口按全局 slug 查重，已存在就拒绝。
- frontmatter 若写 `category:`，必须与上传时填写的分类完全一致；一般不写。

## index.md

```markdown
---
date: 2026-10-03
updated: 2026-10-03
summary: 一句话摘要
tags: [标签一, 标签二]
aliases: [别名]
draft: false
---

# 标题

正文……

![图片说明](./figure-1.png)
```

- 不写 `cover`。笔记站忽略封面。
- 标题优先取 `title:`，其次正文第一行 `# H1`（取出后不重复渲染），最后用 slug。
- 没有 `date` 时用文件修改时间排序。`updated` 缺省取 `date`。
- `tags`、`aliases` 可写行内数组或 Obsidian 多行列表，并参与 `[[链接]]` 解析。
- 图片只写 `./文件名`。把 `![[图.png]]` 改成 `![说明](./图.png)`。
- `[[标题或别名]]` 作站内链接；指向尚不存在的笔记会在图谱里显示为虚节点。
- `$…$`、`$$…$$` 直接写。
- `draft: true` 只保存不公开。
- 公开地址 `/post/<slug>`。

## 整理

1. 建 `<slug>/`，正文写入 `index.md`，用到的图片平铺到同层。未被引用的图片不放。
2. 图片文件名改成小写英文加连字符，如 `figure-1.png`，同时改正文引用。
3. Word/pandoc 的 `media/` 子目录图片移到同层，删掉 `{width=...}`。
4. 补 frontmatter，删掉 `cover`。
5. 跑下面的校验。通过后告诉用户文件夹路径和要填写的分类。

除非用户要求，不要直接写进 `Notes/`。正式发布走上传页。

## 校验

```powershell
$dir = '<bundle 路径>'
$slug = Split-Path $dir -Leaf
$items = Get-ChildItem -Force $dir
$img = 'png','jpg','jpeg','gif','webp','avif'
$err = @()
if ($slug -cnotmatch '^[a-z0-9]+(?:-[a-z0-9]+)*$' -or $slug.Length -gt 80) { $err += "slug 不合法: $slug" }
if ($items | Where-Object PSIsContainer) { $err += '存在子文件夹' }
$files = @($items | Where-Object { -not $_.PSIsContainer })
if (@($files | Where-Object Name -ceq 'index.md').Count -ne 1) { $err += '需要恰好一个 index.md' }
foreach ($f in $files) {
  if ($f.Name -ceq 'index.md') { continue }
  if ($f.Extension.TrimStart('.').ToLower() -notin $img) { $err += "不允许的文件: $($f.Name)" }
  if ($f.Name -match '[\s%?#()\[\]]' -or $f.Name.StartsWith('.') -or $f.Name.Length -gt 120) { $err += "文件名不合法: $($f.Name)" }
  if ($f.Length -gt 10MB) { $err += "图片超过 10MB: $($f.Name)" }
}
if ($files.Count -gt 32) { $err += '文件超过 32 个' }
if (($files | Measure-Object Length -Sum).Sum -gt 50MB) { $err += '总大小超过 50MB' }
$md = Get-Content -Raw -Encoding UTF8 (Join-Path $dir 'index.md')
if (-not $md.Trim()) { $err += 'index.md 为空' }
if ($md -match '(?m)^cover:') { $err += '笔记不要写 cover' }
foreach ($m in [regex]::Matches($md, '!\[[^\]]*\]\(\./([^)\s]+)\)')) {
  if (-not (Test-Path -LiteralPath (Join-Path $dir $m.Groups[1].Value))) { $err += "图片引用缺失: $($m.Groups[1].Value)" }
}
if ($md -match '!\[\[') { $err += '存在 Obsidian 嵌入' }
if ($err) { $err } else { 'OK' }
```

再确认 `Notes/*/<slug>` 不存在。
