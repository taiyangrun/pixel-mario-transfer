---
name: pixel-mario-transfer
slug: pixel-mario-transfer
displayName: FC像素马里奥转绘
version: 1.0.0
summary: "把实拍照片一键转成 FC 红白机《超级马里奥》8-bit 像素截图风格：有限色板、粗颗粒像素块、问号砖块与水管、经典 SCORE/COINS/WORLD/TIME 顶部 HUD，附可复用的转绘提示词模板。"
license: MIT
icon: icon.png
description: "Transform real-world reference photos into NES/Famicom Super Mario 8-bit pixel-art screenshot prompts or generated images with maximum 8-bit fidelity. Use when the user provides portrait, street, park, or travel photos and asks for FC pixel Mario screenshot transfer, retro 8-bit style transfer, photo-to-pixel-art prompt writing, image-to-image prompts, question blocks and pipes, or reusable real-photo-to-pixel workflows."
---

# FC像素马里奥转绘

Convert real-world reference photos into **NES/Famicom Super Mario Bros. 8-bit pixel-art screenshots**. The priority is **MAXIMUM 8-BIT PIXEL FIDELITY**: chunky visible pixels, limited NES color palette, tile-based backgrounds — authentic 1985 hardware constraints, not smooth retro illustration, not modern pixel-art polish.

This is a fan-made, non-commercial workflow for personal learning, research, and prompt testing only. It is not affiliated with, endorsed by, sponsored by, or approved by Nintendo, Super Mario Bros., or any related rights holders. Do not use outputs for commercial sale, advertising, merchandising, paid services, or uses that imply official authorization.

## Output Mode

- If the user asks for prompts, return the final prompt in one code block unless they ask for explanation.
- If the user asks to generate images, use the available image generation workflow.
- If generating from a reference photo, generate first, then provide the final prompt unless the user asks for image only.
- If both prompt and image are requested, generate first, then provide the prompt.
- Use Chinese for user-facing final prompts, but keep the English rendering-control blocks exactly because they strongly steer image models.

## Reference Analysis

Before writing the prompt, identify only what affects transfer:

- Core subject: portrait, street, park, building, landscape, pet.
- Recognizable features to preserve: pose, main shapes, color masses, skyline silhouette.
- 8-bit mapping: reduce the scene to tile-grid logic — sky → blue tile background with blocky clouds, ground → brick/ground tiles, people → 16x32-style sprites, objects → question blocks, pipes, bricks.
- Scene type: platform run, underground, castle approach, overworld stroll.
- Detail budget: NES could show ~64 sprites; simplify ruthlessly.

Preserve the reference photo's identity in silhouette and color masses. Simplify it into an 8-bit level, not a pixel painting.

## Planning Workflow

Before filling the final prompt, decide:

1. 场景类型：地上关 / 地下关 / 城堡 / 夜晚版，对应哪种经典关卡氛围
2. 精灵模式：默认将照片人物转译为 8-bit 马里奥式小人（红帽、工装背带裤，SMB1 精灵比例）；或纯场景
3. 关卡元素：问号砖块 / 水管 / 板栗仔 / 金币，按场景点缀
4. HUD：经典顶部 SCORE 000000、COINS ×00、WORLD 1-1、TIME
5. 网格感：所有边缘对齐像素网格，无抗锯齿

Do not output this planning checklist unless the user asks. Reflect the decisions in the final prompt.

## Prompt Template

When a reference image is provided, always derive concrete content from the image. Never output placeholders.

Use this order for prompt-only output and image-generation prompts:

```text
NES Famicom Super Mario Bros 8-bit pixel art screenshot - MAXIMUM 8-BIT PIXEL FIDELITY.
This must look EXACTLY like an actual 1985 NES cartridge screenshot, NOT smooth retro illustration, NOT modern pixel art, NOT a cartoon.

RENDERING STYLE - 8-BIT NES (CRITICAL):
VISIBLE CHUNKY PIXELS, every edge snaps to a pixel grid, NO anti-aliasing; LIMITED NES COLOR PALETTE — flat solid color masses, 3-4 tones per object; tile-based backgrounds repeating in a grid; sprites in classic 16x32 proportions with 2-3 frame readability; simple dithered shading ONLY where the original hardware would; NO gradients, NO smooth shading, NO modern glow effects.

SCENE：保留<参考图核心构图、主体剪影、主色块>，按 8-bit 网格逻辑简化为<关卡类型>；画面尺寸比例：9:16，1440x2560
SPRITE：<默认：照片人物转译为 8-bit 马里奥式小人，红帽、工装背带裤，SMB1 精灵比例>；<一句话写清动作>
LEVEL ELEMENTS：<3-6 个场景适配元素，只列名称，如：问号砖块、水管、板栗仔、金币、城堡>
HUD：顶部经典 HUD：SCORE 000000、COINS ×00、WORLD 1-1、TIME 300，白色像素字体，像游戏内状态

COLOR PALETTE - NES <场景类型>:
Sky: flat SMB blue (#5C94FC-ish solid); Ground: orange-brown brick tiles; limited to authentic NES tones; NO gradients.

TILE GRID - NES HARDWARE:
Background built from repeating 16x16 tiles; clouds and bushes share the same blocky shape language; all edges pixel-aligned.

STRICT SELF-CHECK TARGET:
The final image must pass: chunky visible pixels everywhere, zero anti-aliasing; authentic limited NES palette with flat color masses; characters read as 8-bit SMB-style sprites; classic HUD is game-diegetic, never a poster title; reference silhouette and color masses preserved; no smooth shading, no gradients, no modern pixel-art polish.

FINAL EMPHASIS - MUST LOOK LIKE AN ACTUAL NES SCREENSHOT:
Chunky pixels. Limited palette. Tile grid. NO anti-aliasing, NO gradients, NO modern polish.
```

## Required Prompt Fields

Every final prompt must include:

- Scene description: concrete sprite, action, level type, preserved reference silhouette and color masses.
- Sprite mode: default 8-bit Mario-style sprite, or scene only.
- `COLOR PALETTE`: authentic NES tones, flat masses.
- `TILE GRID`: repeating tiles, pixel-aligned edges.
- `STRICT SELF-CHECK TARGET`: a compact pass/fail target that names chunky pixels, limited palette, sprite style, and reference preservation.
- Opening and final emphasis blocks, unchanged in meaning.

## Style Anchor Rules

Start every image prompt with these two lines:

```text
NES Famicom Super Mario Bros 8-bit pixel art screenshot - MAXIMUM 8-BIT PIXEL FIDELITY.
This must look EXACTLY like an actual 1985 NES cartridge screenshot, NOT smooth retro illustration, NOT modern pixel art, NOT a cartoon.
```

Then include `RENDERING STYLE - 8-BIT NES (CRITICAL)` before scene content. Include `STRICT SELF-CHECK TARGET` before final emphasis. End every prompt with `FINAL EMPHASIS - MUST LOOK LIKE AN ACTUAL NES SCREENSHOT`.

Do not scatter extra style essays across the prompt. Rendering control lives in the opening, color, tile grid, and final emphasis blocks.

## 8-bit Rendering Calibration

Default to SMB1 overworld:

- Flat SMB sky blue, blocky white clouds, orange-brown ground tiles.
- Sprites: 16 wide × 32 tall readability, bold 2-tone shading max.
- HUD: white pixel font, SCORE / COINS / WORLD / TIME top strip.
- Level props: ? blocks, pipes, bricks, flagpole, castle — chunky and iconic.
- Enemies, when present: goombas, koopas — simple, charming, blocky.
- Absolutely no anti-aliasing, no gradients, no bloom.
