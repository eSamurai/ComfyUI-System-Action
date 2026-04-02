# ⚙️ ComfyUI System Action Node (Smart & Safe)

A powerful, asynchronous system management node for ComfyUI. Safely shutdown, restart, or execute custom system commands automatically at the exact end of your batch renders. 

Featuring **Smart Browser Targeting**, it cleanly frees up your RAM and VRAM after long overnight renders without disrupting your other active tasks.

## 🚀 Key Features

* **🎯 Smart Browser Targeting (New!):** When choosing `Close Comfy & SM`, the node dynamically detects ComfyUI's active port (even if changed via `--port`) using native network scanning to find & terminate the browser session along with ComfyUI and StabilityMatrix (if present).
* **🧹 Clean Exit Sequence:** Ensures a perfect cleanup by closing processes in the logical order: Frontend (Browser) ➡️ Launcher (Stability Matrix) ➡️ Backend (ComfyUI python process).
* **⏳ Batch-Aware:** It waits for the *entire* queue to finish. If you queue 100 images, it intelligently monitors the server and only triggers the action after the 100th image is completely done.
* **💻 Native Windows Timers:** Uses official OS timers for `Shutdown` and `Restart`, triggering the standard Windows warning screen. This allows you to easily abort the action (using `shutdown /a` in CMD) if you change your mind.
* **🛡️ Fail-Safe & Non-Blocking:** Runs in a separate background thread so it never freezes the ComfyUI interface. If you don't use Stability Matrix, the node will silently ignore it without throwing any errors.

## 📥 Installation

Navigate to your ComfyUI `custom_nodes` folder and clone this repository:
  ```
  git clone https://github.com/eSamurai/ComfyUI-System-Action.git
  ```
Restart ComfyUI, and you will find the node in the Utils/System category.

## 🛠️ Usage & Node Inputs

Place the System Action Node at the very end of your workflow (e.g., right after your Save Image or Video Combine node). Connect any output line (Image, Latent, or String) to its pass_through input.

## Input	Description
**action:**  Choose from: None, Shutdown, Restart, Close Comfy & SM, or Custom Command.

**delay_seconds:**	Time to wait before executing the action. (e.g., 120 gives you a 2-minute warning before a shutdown).

**custom_command:**	If Custom Command is selected, type any CMD command to execute (e.g., explorer.exe C:\ComfyUI\output to open your renders folder, or anything you like to execute after the queue).

💡 Pro Tips

* Use Close Comfy & SM for overnight rendering. It ensures your GPU and RAM are 100% freed up by the time you wake up.

* To abort a pending Shutdown or Restart, press Win + R, type cmd, and press Enter. Then type shutdown /a and hit Enter.

## ⚠️ Compatibility

This node utilizes Windows-specific commands (taskkill, netstat, shutdown) and is currently exclusively optimized for Windows environments.
