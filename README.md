# CodeGRITS

[[Website]](https://codegrits.github.io/CodeGRITS/)
[[Paper PDF]](https://codegrits.github.io/CodeGRITS/static/paper.pdf)
[[Source Code]](https://github.com/codegrits/CodeGRITS/)
[[Archived]](https://archive.softwareheritage.org/swh:1:dir:your-directory-id)
[[MIT License]](https://github.com/codegrits/CodeGRITS/blob/main/LICENSE)

Ningzhi Tang*, Junwen An*, Meng Chen, Aakash Bansal, Yu Huang, Collin McMillan, and Toby Jia-Jun Li. 2024.
CodeGRITS: A Research Toolkit for Developer Behavior and Eye Tracking in IDE. ICSE 2024 Demo.

## Purpose

[CodeGRITS](https://codegrits.github.io/CodeGRITS/) stands for **G**aze **R**ecording & **I**DE **T**racking **S**ystem,
which is designed for empirical software engineering researchers, especially those interested in studying
developers' programming behaviors. It is a plugin for JetBrains IDEs (IntelliJ, PyCharm, etc.) that collects developer
IDE interactions and eye-tracking data, and exports them into XML files. It also includes several practical features
including screen recording, dynamic configuration, activity labeling, and a real-time API.

### Claiming Badges

1. **Artifacts Available:** The [archive](https://archive.softwareheritage.org/swh:1:dir:your-directory-id) of the
   artifact is available at Software Heritage.
2. **Artifacts Evaluated – Reusable:** The artifact is very carefully documented on
   the well-structured [website](https://codegrits.github.io/CodeGRITS/).
   The [source code](https://github.com/codegrits/CodeGRITS/) is available at GitHub and is consistent and complete.
   Thorough [instructions](https://codegrits.github.io/CodeGRITS/usage-guide/) are provided for setting up the artifact
   and reproducing the results.
3. **Results Reproduced:** Through our provided instructions or [prepared VM image](), the results can be easily
   reproduced.

## Provenance

- [VirtualBox VM image](): Please download it from Google Drive.
- [Archived artifact](https://archive.softwareheritage.org/swh:1:dir:your-directory-id): We archive the artifact at
  Software Heritage.
- [Paper PDF](https://codegrits.github.io/CodeGRITS/static/paper.pdf): The paper is available at the website.

## Setup

### Hardware Requirements

The VirtualBox VM image (named `UbuntuVM`) requires 8GB of base memory and 4 CPU cores. Its disk size is 27.5GB. Thus,
the host computer should have such hardware resources available.

The PC that has a [Tobii Pro Fusion](https://www.tobii.com/products/eye-trackers/screen-based/tobii-pro-fusion) eye
tracker is preferred, but not required. CodeGRITS could use the mouse to
simulate the eye tracker. We believe it would not affect the evaluation results.

### Software Requirements

We use the VirtualBox 7.0.12 for Windows hosts downloaded
from [here](https://download.virtualbox.org/virtualbox/7.0.12/VirtualBox-7.0.12-159484-Win.exe).
But we expect the version of it is not important, as long as it is not too old.

The OS of VM is Ubuntu 20.04 LTS. CodeGRITS is a plugin developed for JetBrains IDEs. We install IntelliJ IDEA Community
Edition 2023.2 in the VM.

## Usage

### Basic Usage

1. Login to the VM with the username `sandwich` and password `sandwich123`.
2. Open the CML terminal (e.g., `Ctrl+Alt+T`) and run the following commands to start the IntelliJ IDEA.
   ```shell
   cd ~/idea-IC-232.10227.8/bin
   ./idea.sh
   ```
3. We prepared a demo project in the `~/IdeaProjects/HelloWorld` directory. If it is not opened automatically, please
   open it manually in the IntelliJ IDEA.
4. Click the `Tools` on the menu bar, the three buttons `Start Tracking`, `Pause Tracking (inactive)`,
   and `Configuration` should be visible. It means we have successfully installed the CodeGRITS plugin.

### Detailed Usage

#### Configuration

Click the `Tools -> Configuration` button on the menu bar. The configuration window should be opened.
Just as the documentation says, we can select the eye tracker, set attributes, and pre-set labels.
We have already set them for the testing, so you could just click the `OK` button to close the window, or play with it
if you are interested.

We have selected all three trackers. If you have a Tobii Pro Fusion eye tracker, you could connect it to
the VM and select it in the `Eye Tracker Device` drop-down list. We also installed the calibration software
[Tobii Pro Eye Tracker Manager](https://www.tobii.com/products/software/applications-and-developer-kits/tobii-pro-eye-tracker-manager#downloads)
in the VM. You could open it via the following command in the terminal.

```shell
cd /usr/bin
tobiiproeyetrackermanager
```

But you are recommended to use `Mouse` as a substitute, because it is (1) more convenient and does not affect the
usability of the artifact, and (2) the calibration results will not be accurate when using VM.

The Python Interpreter Path is set to `/home/sandwich/anaconda3/envs/codegrits/bin/python`, which contains 
all required Python packages.

#### Tracking

Click the `Tools -> Start Tracking` button on the menu bar. Then play something with the IDE just like you are
programming. For example, you could move the mouse cursor, run the class, edit the code, close the file, etc.
Or use some fancy features of the IDE, such as go to the declaration, reformat the code, etc.

To test the "Add Labels" feature, you could right-click in the editor, and click `Add Label --> Fixed Bug x.y`.
Then a notification should be shown in the bottom-right corner. The label should be added to
the `ide_tracking.xml/<actions>`.

You could test `Tools -> Pause Tracking` then `Tools -> Resume Tracking`, the data during the pause should be skipped.

After playing with the code for a while, click the `Tools -> Stop Tracking` button on the menu bar. After a refresh
of the IDE, the data should be exported to the root directory of the project (configured before). The directory name
is the start timestamp (e.g., 1703733884206). You could see the exported data in the following structure.
See more details at [Data Format](https://codegrits.github.io/CodeGRITS/data-format/).

```angular2html
[OUTPUT_DIR]
├── [START_TIMESTAMP]
│   ├── ide_tracking.xml
│   ├── eye_tracking.xml
│   ├── archives
│   │   ├── [ARCHIVE_TIMESTAMP_1].archive
│   │   ├── [ARCHIVE_TIMESTAMP_2].archive
│   │   ├── ...
│   ├── screen_recording
│   │   ├── clip_1.mp4
│   │   ├── clip_2.mp4
│   │   ├── ...
│   │   ├── frames.csv
```

Browse the data files, especially the `ide_tracking.xml` (<actions> is the most important part),
and `eye_tracking.xml`. They successfully record your IDE interactions and eye gazes (i.e., mouse locations).

#### Real-time Data API

===== TODO =====