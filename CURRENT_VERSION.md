> 上游历史资料：本项目已 fork 为叠意（dyth_homepage），当前入口说明见 [README.html](README.html)。本文中的原公司名称、CloudBase 环境、线上地址与回退路径属于上游项目，不是本项目的发布配置。

# Current rollback version

## V9

- Approved snapshot: `versions/v9-approved-20261015/`
- Recorded on: 2026-10-15 (Asia/Shanghai)
- Status: current approved rollback point

This snapshot is the current approved rollback point captured before the post-V9 To C palette update. It includes the post-V8 mobile-responsive repair: all five hero capability labels remain visible on phones, mobile navigation and spacing are optimized, fixed card heights are reduced, and horizontal overflow is prevented.

The currently deployed To C page also includes post-V9 updates: a unified warm-white, pale blue-gray, and Tencent-blue palette while retaining the original blue, orange, green, and yellow product-card colors; a generated 3D IP founder portrait for Karmatang; and a five-card Green Book series section. WorkBuddy, Codex, TraeWork and Qoder now open their own reading pages with 慢漫 and 小明同学 IP images on their covers and concise copyright/disclaimer and thanks sections. The “MORE” card shows the supplied 豆包工作、百度搭子 and 千问办公 logos as upcoming subjects. Both To C and To B now use the supplied blue YMSH symbol in their navigation and the complete company logo in their footer; the four Green Book covers use the white symbol. These updates have not been assigned a new version label. See `VERSIONS.md` for the 2026-10-19 deployment records and backups.

On 2026-10-20, all eight public HTML pages received the supplied blue YMSH symbol as their browser-tab icon. This post-V9 update is recorded in `VERSIONS.md` with a complete local pre-publish snapshot at `versions/pre-favicon-20261020/`. It has not been assigned a new version label.

## Restore

1. Replace the contents of `dist/` with the contents of `versions/v9-approved-20261015/`.
2. Deploy `dist/` to CloudBase environment `ymsh-team-d7ghsmmwt6c4e3b01`.
