> 上游历史资料：本项目已 fork 为叠意（dyth_homepage），当前入口说明见 [README.html](README.html)。本文中的原公司名称、CloudBase 环境、线上地址与回退路径属于上游项目，不是本项目的发布配置。

# Website versions

## V9 · Current approved rollback version

- Complete snapshot: `versions/v9-approved-20261015/`
- To C homepage: `versions/v9-approved-20261015/index.html`
- To B enterprise page: `versions/v9-approved-20261015/enterprise.html`
- To C SHA-256: `5cca6f71a0110048f60b908e238cb42f4bd9e9edb8d48a208c6b9562039a1d64`
- To B SHA-256: `2ec069f10e2a5bdbe2c38e3b563943103238dd01bb4f3b0c3a8d45084ce628df`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public To C URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Public To B URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html`
- Recorded on: 2026-10-15 (Asia/Shanghai)

V9 is the current approved rollback snapshot captured before the post-V9 To C palette update. It includes all V8 content and interactions plus the mobile-responsive repair: the five hero capability labels use a compact simultaneous floating layout instead of phone-only rotation, mobile navigation has larger touch targets, product and enterprise cards use more compact responsive heights and spacing, and horizontal overflow is prevented.

To restore V9, replace the contents of `dist/` with the complete contents of `versions/v9-approved-20261015/`, then deploy `dist/` to the CloudBase environment above.

### Post-V9 deployed update · Unified To C palette

- Deployed on: 2026-10-15 (Asia/Shanghai)
- Scope: To C visual presentation only; To B and the V9 snapshot remain unchanged
- Current To C SHA-256: `eb1d7884c051d380e0df203676e080112198f91e8b51709582d23f6eea880806`
- CloudBase verification: 33/33 files uploaded and verified
- CloudBase pre-publish backup: `.cloudbase-backup/1792047491294/`

This update brings the To C sections into a more consistent warm-white, pale blue-gray, and Tencent-blue visual family. The “正在做的产品” cards deliberately retain their original blue, orange, green, and yellow backgrounds so the product area remains lively and easy to scan. Desktop and 390-pixel mobile layouts were checked, with no console errors or horizontal overflow. It has not been assigned a new version label.

### Post-V9 deployed update · Karmatang IP founder portrait

- Deployed on: 2026-10-16 (Asia/Shanghai)
- Scope: To C “我们是谁” section only; To B and the V9 snapshot remain unchanged
- Current To C SHA-256: `1af100ac3ddd1823d867dd2abe0d35b81ea8788c3c748e5bae355b69761d3dd5`
- Generated asset: `dist/assets/founder-karmatang-ip-20261016.png`
- Asset SHA-256: `caac923d04a8be747398059f41f62827fd3f5c78dec2cb26f107c75559f7a3ec`
- CloudBase verification: 34/34 files uploaded and verified
- CloudBase pre-publish backup: `.cloudbase-backup/1792131862552/`

This update replaces Karmatang's former photo with a generated 3D IP founder portrait based on the supplied character turnaround: black tousled hair, black techwear jacket, white inner layer, and restrained cyan technology accents in a bright AI product workspace. Desktop and 390-pixel mobile crops were checked, with no console errors or horizontal overflow. It has not been assigned a new version label.

### Post-V9 deployed update · Green Book series

- Deployed on: 2026-10-17 (Asia/Shanghai)
- Scope: To C homepage navigation and Green Book section only; To B is unchanged
- Current To C SHA-256: `4c415404823232fd7a0ccc403ecefb988b26855b0373df5fa3f851ab25ee17ba`
- Added assets: `dist/assets/greenbook-workbuddy-logo.png`, `dist/assets/greenbook-codex-logo.png`, `dist/assets/greenbook-traework-logo.png`, `dist/assets/greenbook-qoder-logo.png`
- CloudBase verification: 38/38 files uploaded and verified
- CloudBase pre-publish backup: `.cloudbase-backup/1792218450116/`
- Local pre-publish snapshot: `versions/pre-greenbooks-20261017/`

This update adds a Green Book navigation entry and a five-card Green Book series between Products and Notes: WorkBuddy, Codex, TraeWork, Qoder, and an upcoming-guides card. Desktop uses one compact five-card row; tablet and mobile preserve one row with horizontal swipe and no page-level overflow. The four product logos use compact square treatments, and the books intentionally remain non-clickable while in preparation. Desktop and 390-pixel mobile layouts were checked with no console errors. It has not been assigned a new version label.

### Post-V9 deployed update · Three Green Book reading pages

- Deployed on: 2026-10-17 (Asia/Shanghai)
- Scope: To C Green Book cards and three new reading pages; To B is unchanged
- Current To C SHA-256: `62add51b20b6cdc207a4ccfd7f9bd847ba4e6db45fcd003d106cf993e6125e6e`
- WorkBuddy page SHA-256: `a028fa575f9938cf82a219feadec6ffb918d32a359b96132485f5f5d977056ab`
- Codex page SHA-256: `31c1af98adba4bae5a0ed08965f10585a685d72e603a17db380c03bd393e2963`
- Qoder page SHA-256: `1d5c30f5ddee7448d74d8e73cc797ecd6403338ad7a7cf20fa42774cfe3ff905`
- CloudBase verification: 442/442 files uploaded and verified; the four HTML files above were fetched from the public site and matched their local SHA-256 values
- CloudBase pre-publish backup: `.cloudbase-backup/1792227323473/`
- Local pre-publish snapshot: `versions/pre-greenbook-pages-20261017/`

WorkBuddy, Codex and Qoder cards now link to `workbuddy-greenbook.html`, `codex-greenbook.html` and `qoder-greenbook.html`. TraeWork remains in preparation. Each book has a table of contents, a return link to the To C Green Book section, an editorial reading note and local images. Referenced book assets were reduced from about 132 MiB to 56 MiB with lossless WebP conversion where possible; one source PNG that the converter could not decode was re-exported as JPEG. This update has not been assigned a new version label.

### Post-V9 deployed update · Green Book covers and frontmatter

- Deployed on: 2026-10-19 (Asia/Shanghai)
- Scope: To C Green Book upcoming card and WorkBuddy, Codex, Qoder reading pages; To B is unchanged
- To C homepage SHA-256: `9f9d405a7e1ab886d2d5e346a873f6dc51d26830bfccd0bb3dfb812759f21337`
- WorkBuddy page SHA-256: `1013646439b9508a555525382a190d409ed9fe8c7aa1d781c1655283d6a16422`
- Codex page SHA-256: `b501e615ba3f248c6fee0e5a8cb12355028430c053ebe8b54836cf682350cc18`
- Qoder page SHA-256: `19e9573541c94ac910caafc7c0f440747f7d358618eb62a655f41f98902a6f01`
- CloudBase verification: 444/444 files uploaded and verified; the homepage, three book pages, shared stylesheet and two new IP images were fetched from the public site and matched local SHA-256 values
- CloudBase pre-publish backup: `.cloudbase-backup/1792396809076/`
- Local pre-publish snapshot: `versions/pre-greenbook-frontmatter-ip-20261019/`

The upcoming card now says “豆包工作等其他绿皮书正在筹备”. The three published books show 慢漫 and 小明同学 IP images on the cover, followed by concise copyright/disclaimer and thanks sections. This update has not been assigned a new version label.

### Post-V9 deployed update · TraeWork Green Book reading page

- Deployed on: 2026-10-19 (Asia/Shanghai)
- Scope: To C Green Book intro/card and a new TraeWork reading page; To B and the V9 snapshot remain unchanged
- To C homepage SHA-256: `022b2e8c63d11f65f5b784db57d261473312981ff3edbf8493088d727510935a`
- TraeWork page SHA-256: `48991f9077a0766e918c81cebc39f229646cc00beebb5ee050fdccd39e0cdc3c`
- CloudBase verification: 703/703 files uploaded and verified; the homepage, new reading page, two IP images and a referenced chapter image matched their local SHA-256 values when fetched from the public site
- CloudBase pre-publish backup: `.cloudbase-backup/1792409274468/`
- Local pre-publish snapshot: `versions/pre-traework-greenbook-20261019/`

The TraeWork card now opens `traework-greenbook.html` from anywhere on the card. The nine-chapter, 31-section guide uses a practical reading path, locally hosted illustrations, the 慢漫 and 小明同学 cover images, and concise copyright/disclaimer and thanks sections. Editorial updates remove time-sensitive model rankings, clarify the current TRAE product naming, and add credential and third-party integration cautions. This update has not been assigned a new version label.

### Post-V9 deployed update · Upcoming Green Book logos

- Deployed on: 2026-10-19 (Asia/Shanghai)
- Scope: To C Green Book “MORE” card only; To B and the V9 snapshot remain unchanged
- To C homepage SHA-256: `7f635f5d9e2bdb9ff8e2abc9c26bd4dcc5a3f4f6b6d0d0c25db8c8d7dc549ebd`
- Added assets: `dist/assets/greenbook-more-doubao.jpg`, `dist/assets/greenbook-more-baidu.png`, `dist/assets/greenbook-more-qianwen.jpg`
- CloudBase verification: 706/706 files uploaded and verified; the homepage and three new logos matched their local SHA-256 values when fetched from the public site
- CloudBase pre-publish backup: `.cloudbase-backup/1792412346711/`

The card now shows the supplied logos with labels for 豆包工作、百度搭子 and 千问办公, and its heading reads “其他绿皮书正在筹备”. Desktop and 390-pixel mobile layouts were checked. This update has not been assigned a new version label.

### Post-V9 deployed update · YMSH brand logos

- Deployed on: 2026-10-19 (Asia/Shanghai)
- Scope: To C and To B header/footer branding, plus the covers of four published Green Books
- To C homepage SHA-256: `160803d18c5ff91ba7972a450cceb3b802040e99450f5ab87c478e9486dd3e2e`
- To B homepage SHA-256: `e81fbb2c8f482d402b933fa08268698b7b82ee475e03529e7c36d96cb192c9b1`
- Added assets: `dist/assets/ymsh-logo-full.png`, `dist/assets/ymsh-logo-blue.png`, `dist/assets/ymsh-logo-white.png`
- CloudBase verification: 709/709 files uploaded and verified; both homepages, four Green Book pages, the shared stylesheet and all three logo files matched their local SHA-256 values when fetched from the public site
- CloudBase pre-publish backup: `.cloudbase-backup/1792420793925/`

The blue symbol replaces the former “山” badge in both main navigations. The complete wordmark appears in both footers, while the white symbol replaces the letter medallion at the bottom of each Green Book cover. Desktop and 390-pixel mobile layouts were checked. This update has not been assigned a new version label.

### Post-V9 deployed update · Unified YMSH browser-tab icons

- Deployed on: 2026-10-20 (Asia/Shanghai)
- Scope: all eight public HTML pages: To C, To B, course, community, and four Green Books
- Change: replace four old inline SVG favicons and add explicit icons to the four Green Book pages. All eight now reference `assets/ymsh-logo-blue.png?v=20261020`.
- To C homepage SHA-256: `f42268e84eee960bcb28d72858b9f8ba34d80fce2fb64a1944d1d81177956317`
- To B homepage SHA-256: `cf8ac3c24ee7c751e49417b6e93b012529480c09cbc36c3a0982b2f62ee35f9c`
- Course page SHA-256: `43e48de3b7e67160426fc61f8e1561e7e821e694ee49c756264b975b96016d8b`
- Community page SHA-256: `118c7d1091ea9bc2fd23fc985b87afbd6e5f449498789c778c7a5302dc5e91bc`
- WorkBuddy page SHA-256: `066dacf607c838cfb25f710beba91158c871cc47d143bfffb7477ff228801536`
- Codex page SHA-256: `2d7936ff95aed2e063a41b19235aaa2fd12d3fed18d375e1695a58ad6387eee8`
- TraeWork page SHA-256: `293c604b2334352ee44789813b3cbf0034bd52e691a7be2b9700748acb98eb4e`
- Qoder page SHA-256: `085705d6d9038bdac976070d7a187412d2124ce1401e6a7b1f2e569a8fd8e6c2`
- Icon asset SHA-256: `577b2521ff148aee75c35dd782d8db47ac444ada692c69b08b8f52357c08f264`
- CloudBase verification: 709/709 files uploaded and verified; all eight public HTML files and the shared icon asset were fetched from the public site and matched local SHA-256 values.
- CloudBase pre-publish backup: `.cloudbase-backup/1792486206947/`
- Local complete pre-publish snapshot: `versions/pre-favicon-20261020/`

The query parameter helps browsers request the updated favicon URL rather than reusing a cached old tab icon. No page content, styles, or site navigation changed. V9 remains the last user-named approved rollback version.

## V8 · Earlier approved rollback version

- Complete snapshot: `versions/v8-approved-20261013/`
- To C homepage: `versions/v8-approved-20261013/index.html`
- To B enterprise page: `versions/v8-approved-20261013/enterprise.html`
- To C SHA-256: `11aed87a4cf704c6dec8b9e607977ba3adcce5dafb28edb733167d8b34d02a43`
- To B SHA-256: `6d9ba55f3607b75b9d64d097a72e24b466601fcb62381a45f1b5a429c1198ac8`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public To C URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Public To B URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html`
- Recorded on: 2026-10-13 (Asia/Shanghai)

V8 is the approved snapshot captured before the post-V8 mobile-responsive repair. It includes the To C and To B hero capability/knowledge labels and their original mobile rotation, the To B “小程序” capability, plus all product content, assets, and interactions present at capture time.

To restore V8, replace the contents of `dist/` with the complete contents of `versions/v8-approved-20261013/`, then deploy `dist/` to the CloudBase environment above.

### Post-V8 deployed update · Mobile responsive repair

- Deployed on: 2026-10-13 (Asia/Shanghai)
- Scope: To C and To B responsive presentation only; V8 snapshot remains unchanged
- CloudBase verification: 33/33 files uploaded and verified
- CloudBase pre-publish backup: `.cloudbase-backup/1791894201641/`

This update replaces the phone-only carousel treatment for hero capability labels with a compact five-label floating layout, prevents horizontal overflow, improves mobile navigation touch targets, and reduces excessive fixed heights and spacing in product, service, delivery, and case cards. It has not been assigned a new version label.

## V4 · Earlier approved rollback point

- Complete snapshot: `versions/v4-approved-20261009/`
- To C homepage: `versions/v4-approved-20261009/index.html`
- To B enterprise page: `versions/v4-approved-20261009/enterprise.html`
- To C SHA-256: `faa7cd3941c16997c1d64165afe58f2cf92ed49039fd5ca17517b2f3edb607d9`
- To B SHA-256: `dc65b831d59290c79c0419920274bd166287c174e352c6e689f8d274f3820871`
- Current Wise photo SHA-256: `ca73724b60e2d142ed6a57692b2e94c5808908207d772d0a085d91ab0156ea8e`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public To C URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Public To B URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html`
- Recorded on: 2026-10-09 (Asia/Shanghai)

This is the user-designated official V4 rollback point. It contains the complete currently deployed To C and To B website, including the latest Wise WorkBuddy photo with the approved crop, the integrated To C/To B navigation, and the enterprise-page interactions. Earlier `V4 Integrated To C + To B` and `V5 Enterprise Interactions` entries below are retained as historical development snapshots; they do not replace this official V4 label.

To restore official V4, replace the contents of `dist/` with the complete contents of `versions/v4-approved-20261009/`, then deploy `dist/` to the CloudBase environment above.

## V1

- Baseline file: `versions/v1/index.html`
- Original deployed file MD5: `e26b66d117a51f30545b1132f1b70b10`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Recorded on: 2026-10-07 (Asia/Shanghai)

V1 is the copy approved immediately before the walking-penguin animation and footer cleanup.

## V2

- Baseline file: `versions/v2/index.html`
- Walking sprite: `versions/v2/assets/qq-penguin-walk-sprite.png`
- Deployed file MD5: `21f95e78f7508c61bdbe5c39073e0cee`
- Sprite MD5: `f15a5190559974e4c3a1dca8d2d460df`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Recorded on: 2026-10-07 (Asia/Shanghai)

V2 includes the four-frame walking penguin, Tencent-blue topic highlighting that follows its position, a smaller above-text walking track, and the simplified footer.

## V3

- Complete snapshot: `versions/v3/`
- Homepage: `versions/v3/index.html`
- Course page: `versions/v3/course.html`
- Community page: `versions/v3/community.html`
- All site assets: `versions/v3/assets/`
- Homepage MD5: `f9252f212aedcab47daecd28d53b331a`
- Course page MD5: `f33dac91f547a057c95d1f19afb01dc5`
- Community page MD5: `607f846d0df28ac64eaa0dc06202452d`
- Shared secondary-page CSS MD5: `3a3880c4a225550b4d13c997eba05312`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/`
- Recorded on: 2026-10-08 (Asia/Shanghai)

V3 is the complete approved website after the course and community secondary pages, founder photos, QR codes, six linked articles, Tencent-blue learning-card interaction, unified `逸鸣山海Team` naming, and the enterprise AI enablement card were added. The course consultation and community application buttons return to the homepage contact section.

To restore V3, replace the contents of `dist/` with the complete contents of `versions/v3/`, then deploy `dist/` to the CloudBase environment above.

## To B V1

- Standalone preview: `versions/to-b-v1/index.html`
- Recorded on: 2026-10-08 (Asia/Shanghai)

To B V1 is an undeployed HTML concept that shifts the narrative from the founders and consumer offerings to the company, enterprise AI services, delivery method, business scenarios, and proof from real operating practice. It reuses selected V3 assets through relative paths.

## V4 Integrated To C + To B

- Complete deployed snapshot: `versions/v4-integrated/`
- To C homepage: `versions/v4-integrated/index.html`
- To B enterprise page: `versions/v4-integrated/enterprise.html`
- To C SHA-256: `0da1661db35330c9575f6edf0138fa9a65cfe7e34e090695d66f47fb363db6d7`
- To B SHA-256: `179125d9909d3d2f4b783ec842fce5c34a435c9fa2638a3f7e420f2261a01533`
- CloudBase environment: `ymsh-team-d7ghsmmwt6c4e3b01`
- Public To C URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/index.html`
- Public To B URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html`
- Recorded and deployed on: 2026-10-08 (Asia/Shanghai)

V4 keeps the existing To C URL, adds the To B enterprise page on the same CloudBase site, provides reciprocal header navigation (`企业服务` / `个人与学习`), and directs the To C enterprise-service card to the new enterprise page. The CloudBase publish completed with pre-publish backup and remote consistency verification.

## V5 Enterprise Interactions

- Complete deployed snapshot: `versions/v5-enterprise-interactions/`
- Enterprise page SHA-256: `dc65b831d59290c79c0419920274bd166287c174e352c6e689f8d274f3820871`
- Feishu QR SHA-256: `5ee13cc5e1547ee00f61324de119746d5ab9f488b0a4085d1f71af0ab0cb89ff`
- Public To B URL: `https://ymsh-team-d7ghsmmwt6c4e3b01-1301792998.tcloudbaseapp.com/enterprise.html`
- Recorded and deployed on: 2026-10-08 (Asia/Shanghai)

V5 adds the Feishu contact QR beside WeChat, interactive Tencent-blue focus states for enterprise services, lift feedback for proof cards, and a walking-penguin delivery timeline that highlights the current step. Narrow layouts use sequential step emphasis instead of a horizontal walker. The CloudBase publish completed with backup and remote consistency verification.
