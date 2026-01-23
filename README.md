# AAE5303 Environment Setup Report — Template for Students

> **Important:** Follow this structure exactly in your submission README.  
> Your goal is to demonstrate **evidence, process, problem-solving, and reflection** — not only screenshots.

---

## 1. System Information

**Laptop model:**  
_[XiaoXinPro14 |AH10]_

**CPU / RAM:**  
_[Intel(R) Core(TM) Ultra 5 225H (1.70 GHz), 32GB RAM]_

**Host OS:**  
_[Windows 11]_

**Linux/ROS environment type:**  
_[Choose one:]_
- [ ] Dual-boot Ubuntu
- [ ] WSL2 Ubuntu
- [ ] Ubuntu in VM (UTM/VirtualBox/VMware/Parallels)
-   Docker container
- [ ] Lab PC
- [ ] Remote Linux server

---

## 2. Python Environment Check

### 2.1 Steps Taken

Describe briefly how you created/activated your Python environment:

I created and activated a Python virtual environment using the venv module. In the project directory, I ran python3 -m venv .venv to create the virtual environment. I then activated it with source .venv/bin/activate. After activation, I installed the required dependencies by running pip install -r requirements.txt. The setup followed the standard procedure with no deviations from the default instructions.

**Tool used:**  
_[venv]_

**Key commands you ran:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  
_[None]_

### 2.2 Test Results

Run these commands and paste the actual terminal output (not just screenshots):

```bash
python scripts/test_python_env.py
```

**Output:**
```
[========================================
AAE5303 Environment Check (Python + ROS)
Goal: help you verify your environment and understand what each check means.
========================================

Step 1: Environment snapshot
  Why: We capture platform/Python/ROS variables to diagnose common setup mistakes (especially mixed ROS env).
Step 2: Python version
  Why: The course assumes Python 3.10+; older versions often break package wheels.
Step 3: Python imports (required/optional)
  Why: Imports verify packages are installed and compatible with your Python version.
Step 4: NumPy sanity checks
  Why: We run a small linear algebra operation so success means more than just `import numpy`.
Step 5: SciPy sanity checks
  Why: We run a small FFT to confirm SciPy is functional (not just installed).
Step 6: Matplotlib backend check
  Why: We generate a tiny plot image (headless) to confirm plotting works on your system.
Step 7: OpenCV PNG decoding (subprocess)
  Why: PNG decoding uses native code; we isolate it so corruption/codec issues cannot crash the whole report.
Step 8: Open3D basic geometry + I/O (subprocess)
  Why: Open3D is a native extension; ABI mismatches can segfault. Subprocess isolation turns crashes into readable failures.
Step 9: ROS toolchain checks
  Why: The course requires ROS tooling. This check passes if ROS 2 OR ROS 1 is available (either one is acceptable).
  Action: building ROS 2 workspace package `env_check_pkg` (this may take 1-3 minutes on first run)...
  Action: running ROS 2 talker/listener for a few seconds to verify messages flow...
Step 10: Basic CLI availability
  Why: We confirm core commands exist on PATH so students can run the same commands as in the labs.

=== Summary ===
✅ Environment: {
  "platform": "Linux-6.6.87.2-microsoft-standard-WSL2-x86_64-with-glibc2.35",
  "python": "3.10.12",
  "executable": "/tmp/PolyU-AAE5303-env-smork-test/.venv/bin/python",
  "cwd": "/tmp/PolyU-AAE5303-env-smork-test",
  "ros": {
    "ROS_VERSION": "2",
    "ROS_DISTRO": "humble",
    "ROS_ROOT": null,
    "ROS_PACKAGE_PATH": null,
    "AMENT_PREFIX_PATH": "/opt/ros/humble",
    "CMAKE_PREFIX_PATH": null
  }
}
✅ Python version OK: 3.10.12
✅ Module 'numpy' found (v2.2.6).
✅ Module 'scipy' found (v1.15.3).
✅ Module 'matplotlib' found (v3.10.8).
✅ Module 'cv2' found (v4.13.0).
✅ Module 'rclpy' found (vunknown).
✅ numpy matrix multiply OK.
✅ numpy version 2.2.6 detected.
✅ scipy FFT OK.
✅ scipy version 1.15.3 detected.
✅ matplotlib backend OK (Agg), version 3.10.8.
✅ OpenCV OK (v4.13.0), decoded sample image 128x128.
✅ Open3D OK (v0.19.0), NumPy 2.2.6.
✅ Open3D loaded sample PCD with 8 pts and completed round-trip I/O.
✅ ROS 2 CLI OK: /opt/ros/humble/bin/ros2
✅ ROS 1 tools not found (acceptable if ROS 2 is installed).
✅ colcon found: /usr/bin/colcon
✅ ROS 2 workspace build OK (env_check_pkg).
✅ ROS 2 runtime OK: talker and listener exchanged messages.
✅ Binary 'python3' found at /tmp/PolyU-AAE5303-env-smork-test/.venv/bin/python3

All checks passed. You are ready for AAE5303 🚀]
```

```bash
python scripts/test_open3d_pointcloud.py
```

**Output:**
```
[ℹ️ Loading /tmp/PolyU-AAE5303-env-smork-test/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /tmp/PolyU-AAE5303-env-smork-test/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.]
```

**Screenshot:**  
_[Include one screenshot showing both tests passing]_

<img width="1377" height="1170" alt="屏幕截图 2026-01-21 173308" src="https://github.com/user-attachments/assets/4a5f25e4-089b-48b2-8537-1d343571eaa6" />

---

## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Paste the build output summary (final lines only):

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output:**
```
Summary: 1 package finished [x.xx s]
```

**Your actual output:**
```
[Starting >>> env_check_pkg
Finished <<< env_check_pkg [0.14s]

Summary: 1 package finished [0.41s]]
```

### 3.2 Run talker and listener

Show both source commands:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Then run talker:**
```bash
ros2 run env_check_pkg talker.py
```

**Output (3–4 lines):**
```
[[INFO] [1768988170.975756230] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1768988171.121119842] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1768988171.671096292] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
[INFO] [1768988172.221032716] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #2']
```

**Run listener:**
```bash
ros2 run env_check_pkg listener.py
```

**Output (3–4 lines):**
```
[[[INFO] [1768497979.743179487] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
[INFO] [1768497979.891195835] [env_check_pkg_listener]: I heard: 'AAE5303 hello #25'
[INFO] [1768497980.252482710] [env_check_pkg_listener]: I heard: 'AAE5303 hello #26'
[INFO] [1768497980.725733843] [env_check_pkg_listener]: I heard: 'AAE5303 hello #27']]
```

**Alternative (using launch file):**
```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
_[Include one screenshot showing talker + listener running]_

<img width="1376" height="927" alt="屏幕截图 2026-01-21 174324" src="https://github.com/user-attachments/assets/9bdc4513-f567-4d97-a478-5de9ea7fd751" />

---

## 4. Problems Encountered and How I Solved Them

> **Note:** Write 2–3 issues, even if small. This section is crucial — it demonstrates understanding and problem-solving.

### Issue 1: [OpenCV and Open3D Failed Due to Missing OpenGL Library]

**Cause / diagnosis:**  
_[OpenCV and Open3D require the OpenGL library (libGL.so.1), but these dependencies are missing from the system. In WSL2 or minimal installations, graphics-related libraries may not be installed.]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[apt install -y libgl1-mesa-glx libglib2.0-0]
```

**Reference:**  
_[System dependency requirements in the official documentation of OpenCV and Open3D；Common issues in a minimal WSL2/Ubuntu installation environment]_

---

### Issue 2: [ROS 2 Workspace Build Failed - Missing catkin_pkg Module]

**Cause / diagnosis:**  
_[The ROS 2 build system (ament_cmake) requires catkin_pkg to parse package.xml. This module is not installed in the virtual environment, and colcon is using the Python from the virtual environment.]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[source .venv/bin/activate；pip install catkin_pkg]
```

**Reference:**  
_[ROS 2 build system documentation (ament_cmake)；colcon build tool requirements]_

---

### Issue 3 (Optional): [Incorrect Executable Names - .py Extension Not Needed]

**Cause / diagnosis:**  
_[The talker and listener in env_check_pkg are C++-compiled executables, not Python scripts, so they do not require a .py suffix.
The names of executables in a ROS 2 package are defined in CMakeLists.txt and package.xml.]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[ros2 run env_check_pkg talker
ros2 run env_check_pkg listener]
```

**Reference:**  
_[ROS 2 official documentation: Running nodes；The ros2 pkg executables command output shows the available executables]_

---

## 5. Use of Generative AI (Required)

Choose one of the issues above and document how you used AI to solve it.

> **Goal:** Show critical use of AI, not blind copying.

### 5.1 Exact prompt you asked

**Your prompt:**
```
[I'm trying to build a ROS 2 workspace using colcon build, but I'm getting this error:
Traceback (most last call):
File "/opt/ros/humble/share/ament_cmake_core/cmake/core/package_xml_2_cmake.py", line 22, in <module>
from catkin_pkg.package import parse_package_string
ModuleNotFoundError: No module named 'catkin_pkg'
CMake Error at .../ament_package_xml.cmake:95 (message):
execute_process(...) returned error code 1]
```

### 5.2 Key helpful part of the AI's answer

**AI's response (relevant part only):**
```
[The error occurs because ROS 2's build system (ament_cmake) uses Python scripts that require the `catkin_pkg` module to parse `package.xml` files. Even though ROS 2 uses ament instead of catkin, it still relies on `catkin_pkg` for package metadata parsing.

Since you're using a Python virtual environment, colcon is likely using the Python interpreter from your `.venv`, which doesn't have `catkin_pkg` installed. The system ROS 2 installation might have it, but your virtual environment doesn't.

**Solution:** Install `catkin_pkg` in your virtual environment:
source .venv/bin/activate
pip install catkin_pkg
]
```

### 5.3 What you changed or ignored and why

Explain briefly:
- Did the AI recommend something unsafe?
- Did you modify its solution?
- Did you double-check with official docs?

**Your explanation:**  
_[The AI's explanation matched the error: `catkin_pkg` was missing in the virtual environment. I verified:

1. Checked ROS 2 docs: `catkin_pkg` is a dependency for ament_cmake, even though ROS 2 doesn't use catkin.
2. Verified the diagnosis: Confirmed colcon was using the venv Python by checking `which python3` inside the venv.
3. Applied the solution: Installed `catkin_pkg` in the venv as suggested.
4. No modifications needed: The solution was straightforward and safe—installing a missing Python package.

I didn't need to modify anything because:
- Installing a Python package in a virtual environment is safe and isolated
- The package name and installation method were correct
- The fix directly addressed the root cause]_

### 5.4 Final solution you applied

Show the exact command or file edit that fixed the problem:

```bash
[cd /tmp/PolyU-AAE5303-env-smork-test
source .venv/bin/activate
pip install catkin_pkg]
```

**Why this worked:**  
_[Installing catkin_pkg in the virtual environment made it available to colcon's build scripts. When colcon ran the ament_cmake Python script (package_xml_2_cmake.py), it could import catkin_pkg and parse package.xml. The build then proceeded successfully, confirming the fix.]_

---

## 6. Reflection (3–5 sentences)

Short but thoughtful:

- What did you learn about configuring robotics environments?
- What surprised you?
- What would you do differently next time (backup, partitioning, reading error logs, asking better AI questions)?
- How confident do you feel about debugging ROS/Python issues now?

**Your reflection:**

_[Configuring robotics environments requires understanding the interaction between system libraries, Python virtual environments, and ROS 2's build system. I was surprised that ROS 2 still depends on catkin_pkg even though it uses ament, and that OpenCV/Open3D need OpenGL libraries even for headless operations. Next time, I would read error messages more carefully first (like checking ros2 pkg executables before guessing executable names), verify package dependencies in official docs before installing, and keep a log of all commands run for easier troubleshooting. After solving these issues systematically, I feel more confident debugging ROS/Python problems by tracing errors to their root causes—whether missing system libraries, Python packages, or incorrect command usage—rather than randomly trying fixes.]_

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
_[GAN Yuxin]_

**Student ID:**  
_[25108433G]_

**Date:**  
_[2026/1/22]_

---

## Submission Checklist

Before submitting, ensure you have:

-   Filled in all system information
-   Included actual terminal outputs (not just screenshots)
-   Provided at least 2 screenshots (Python tests + ROS talker/listener)
-   Documented 2–3 real problems with solutions
-   Completed the AI usage section with exact prompts
-   Written a thoughtful reflection (3–5 sentences)
-   Signed the declaration

---

**End of Report**
