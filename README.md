# FC像素马里奥转绘 (`pixel-mario-transfer`) v1.0.0

把实拍照片一键转成 FC 红白机《超级马里奥》8-bit 像素截图风格：有限色板、粗颗粒像素块、问号砖块与水管、经典 SCORE/COINS/WORLD/TIME 顶部 HUD，附可复用的转绘提示词模板。

Transform real-world reference photos into NES/Famicom Super Mario 8-bit pixel-art screenshot prompts or generated images with maximum 8-bit fidelity. Use when the user provides portrait, street, park, or travel photos and asks for FC pixel Mario screenshot transfer, retro 8-bit style transfer, photo-to-pixel-art prompt writing, image-to-image prompts, question blocks and pipes, or reusable real-photo-to-pixel workflows.

## 文件结构

- `SKILL.md` —— skill 定义（含完整转绘提示词配方 / 工作流）
- `agents/openai.yaml` —— agent 配置
- `icon.png` —— skill 定制图标

## 使用方式

将本仓库作为 skill 包使用：把 `SKILL.md`、`agents/`、`icon.png` 放入你的 skill 目录即可。也已同步上架 [skillhub.cn](https://skillhub.cn) 与 ModelScope（魔搭社区），搜 `pixel-mario-transfer` 即可找到。

## 声明

粉丝自制、非商业用途的 prompt 工作流，仅用于个人学习与研究，与相关权利方无关。输出内容请勿用于商业售卖、广告或暗示官方授权的场景。

## License

MIT

> 备注：8-bit 像素风，问号砖块与水管是灵魂。
