# VCam - 开源虚拟相机插件
 
基于 Theos 的 iOS 越狱插件，Hook 系统相机管线，将自定义视频伪装为实时摄像头画面。

## 功能

- 📷 Hook AVCaptureSession 全管线（视频/音频/拍照）
- 🎬 从相册选择视频，循环注入为相机帧
- 🟢 悬浮按钮 UI（可拖拽，贴边吸附）
- ⚙️ 系统设置界面（开关、循环播放）
- 🆓 无卡密、无网络请求、无 UDID 上传

## 编译（GitHub Actions 自动编译）

1. 在 GitHub 创建一个新仓库，如 `username/VCam`
2. 推送本项目：

```bash
cd VCam
git init
git add .
git commit -m "init: VCam virtual camera tweak"
git remote add origin https://github.com/你的用户名/VCam.git
git push -u origin main
```

3. CI 自动触发，编译完成后在 Actions → Artifacts 下载：
   - `VCam-deb` — 完整 deb 安装包
   - `VCam-dylib` — 单独的 dylib 文件
   - `VCam-full` — 全部产物

## 安装

### 方法 1：deb 安装
```bash
# 通过 SSH 传到设备
scp VCam*.deb root@设备IP:/tmp/
ssh root@设备IP "dpkg -i /tmp/VCam*.deb && killall -9 SpringBoard"
```

### 方法 2：手动安装 dylib
```bash
# 复制 dylib 和 plist 到 Substrate 目录
scp VCam.dylib root@设备IP:/Library/MobileSubstrate/DynamicLibraries/
scp VCam.plist root@设备IP:/Library/MobileSubstrate/DynamicLibraries/
ssh root@设备IP "killall -9 SpringBoard"
```

## 使用

1. 安装后任意 App 右上角出现 📷 悬浮按钮
2. 点击 → 「选择视频」→ 从相册选一段视频
3. 点击 → 「开启虚拟相机」
4. 按钮变绿 = 已激活，此时打开任何调用相机的 App 都会看到你的视频

## 要求

- iOS 14.0+
- 越狱环境（unc0ver / checkra1n / Dopamine / palera1n）
- 或 TrollStore

## 技术栈

- Theos + Logos (Objective-C++)
- AVFoundation / CoreMedia / CoreVideo
- MobileSubstrate (Cydia Substrate)

## License

MIT
