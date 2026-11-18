# Documentation

## Report and presentation
| File | Content |
|---|---|
| [`report/Franka_PickPlace_RL_Report.docx`](report/Franka_PickPlace_RL_Report.docx) | Written project report |
| [`report/Franka_PickPlace_RL_Slides.pptx`](report/Franka_PickPlace_RL_Slides.pptx) | Presentation slides |

## 1. Installation (Windows)
1. Create a Python 3.12 virtual environment and install Isaac Sim 6.0.1 and Isaac Lab 3.0, following the Isaac Lab installation guide.
2. Install `rsl-rl-lib==5.0.1`.
3. Install this project's package (from the Isaac Lab folder, with the environment activated):
   ```bat
   isaaclab.bat -p -m pip install -e <repo>\software\application\source\franka_pick_place
   ```

## 2. Usage
`<app>` = `<repo>\software\application`, `<model>` = `<repo>\machine-skills\pick_place_policy\model_7998.pt`

| Step | Command | Time (RTX 4070 Ti) |
|---|---|---|
| Reward unit test | `python <app>\tests\test_reward_math.py` | seconds |
| URDF analysis (no simulator) | `python <app>\scripts\urdf_analysis.py` | ~1 min |
| Watch the robot | `isaaclab.bat -p <app>\scripts\play.py --num_envs 1 --viz kit --checkpoint <model>` (or double-click `watch_robot.bat`) | |
| Test (1,000 episodes) | `isaaclab.bat -p <app>\scripts\eval.py --num_envs 1000 --headless --checkpoint <model>` | ~3 min |
| Train | `isaaclab.bat -p <app>\scripts\train.py --headless --num_envs 4096` | ~3.3 h |
| Training curves | `python <app>\scripts\plot_training.py` | seconds |
| Record a video | `isaaclab.bat -p <app>\scripts\play.py --num_envs 1 --video --video_length 1500 --checkpoint <model>` | ~3 min |

## 3. Troubleshooting
| Symptom | Fix |
|---|---|
| No Isaac Sim window | Add `--viz kit` (Isaac Lab 3.0 runs headless by default). |
| Out of GPU memory | Lower `--num_envs` (e.g. 2048). |
| Success drops right after resuming training | Normal: every episode restarts at once; it recovers within a few dozen iterations. |
