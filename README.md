# CodeGRITS

[[Website]](https://codegrits.github.io/CodeGRITS/) [[Paper PDF]](https://codegrits.github.io/CodeGRITS/static/paper.pdf) [[Source Code]](https://github.com/codegrits/CodeGRITS/) [[Archived]](https://archive.softwareheritage.org/swh:1:dir:8d3350b8efc8e545689565fddf1d8af55371d758) [[VM Image]](https://drive.google.com/file/d/13U2AjbTkbDwzwN-b_AJeQgavkYi2Q8wv/view?usp=drive_link) [[MIT License]](https://github.com/codegrits/CodeGRITS/blob/main/LICENSE) 

Ningzhi Tang\*, Junwen An\*, Meng Chen, Aakash Bansal, Yu Huang, Collin McMillan, and Toby Jia-Jun Li. 2024. CodeGRITS: A Research Toolkit for Developer Behavior and Eye Tracking in IDE. ICSE 2024 Demo.

## Purpose

[CodeGRITS](https://codegrits.github.io/CodeGRITS/) stands for **G**aze **R**ecording & **I**DE **T**racking **S**ystem, which is designed for empirical software engineering researchers, especially those interested in studying developers' programming behaviors. It is a plugin for JetBrains IDEs (IntelliJ, PyCharm, etc.) that collects developer IDE interactions and eye-tracking data, and exports them into XML files. It also includes several practical features including screen recording, dynamic configuration, activity labeling, etc.

### Claiming Badges

1. **Artifacts Available:** The [archive](https://archive.softwareheritage.org/swh:1:dir:8d3350b8efc8e545689565fddf1d8af55371d758) of the artifact is available at Software Heritage.
2. **Artifacts Evaluated – Reusable:** The artifact is very carefully documented on the well-structured [website](https://codegrits.github.io/CodeGRITS/). The [source code](https://github.com/codegrits/CodeGRITS/) is available at GitHub and is consistent and complete. Thorough [instructions](https://codegrits.github.io/CodeGRITS/usage-guide/) are provided for setting up the artifact and reproducing the results.
3. **Results Reproduced:** Through our provided instructions or prepared [VM image](https://drive.google.com/file/d/13U2AjbTkbDwzwN-b_AJeQgavkYi2Q8wv/view?usp=drive_link), the results can be easily reproduced.

## Provenance

- [VirtualBox VM image](https://drive.google.com/file/d/13U2AjbTkbDwzwN-b_AJeQgavkYi2Q8wv/view?usp=drive_link): Please download it from Google Drive. It is a compressed file named `UbuntuVM.zip` (~14.6GB), please upzip it first and use VirtualBox to open it.
- [Archived artifact](https://archive.softwareheritage.org/swh:1:dir:8d3350b8efc8e545689565fddf1d8af55371d758): The artifact is archived at Software Heritage.
- [Paper PDF](https://codegrits.github.io/CodeGRITS/static/paper.pdf): The paper is available at the website.

## Setup

### Hardware Requirements

The VirtualBox VM image (named `UbuntuVM`) requires 8GB of base memory and 4 CPU cores. Its disk size is ~27.5GB. Thus, the host computer should have such resources available.

CodeGRITS can use the mouse to simulate the eye tracker, and it is difficult to set up a real [Tobii Pro Fusion](https://www.tobii.com/products/eye-trackers/screen-based/tobii-pro-fusion) eye tracker in the virtual machine due to inaccurate calibration. Thus, it is **not** required to have a real eye tracker. We also believe it would not affect the evaluation results.

### Software Requirements

We use the VirtualBox 7.0.12 Windows hosts downloaded from [here](https://download.virtualbox.org/virtualbox/7.0.12/VirtualBox-7.0.12-159484-Win.exe). But we expect the version of it is not important, as long as it is not too old.

The OS of VM is Ubuntu 20.04 LTS. CodeGRITS is a plugin developed for JetBrains IDEs. We have installed IntelliJ IDEA Community Edition 2023.2 in the VM.

## Usage

### Basic Usage

1. After setting up the VM, login to it with the username `sandwich` and password `sandwich123`.
2. Open the CML terminal (e.g., `Ctrl+Alt+T`) and run the following commands to start the IntelliJ IDEA.
   ```shell
   cd ~/Downloads/idea-IC-232.10227.8/bin
   ./idea.sh
   ```
3. We prepared a test project in the `~/IdeaProjects/HelloWorld` directory. If it is not opened automatically, please open it manually in the IntelliJ IDEA.
4. Click the `Tools` on the menu bar, the three buttons `Start Tracking`, `Pause Tracking (inactive)`, and `Configuration` should be visible. It means we have successfully installed the CodeGRITS.
5. We have prepared a sample exported data in the `./1703910153511` directory. You can take it as a reference.

### Detailed Usage

#### Configuration

Click the `Tools -> Configuration` button on the menu bar. The configuration window should be opened. We have selected all three trackers, and set the attributes and pre-set labels for the testing. Click `OK` button to close the window, or play with it if you are interested.

The "Python Interpreter Path" is set to `/home/sandwich/anaconda3/envs/codegrits/bin/python`, which contains all required Python libraries. Please do not change it.

If you have a Tobii Pro Fusion eye tracker, you can find it in the "Eye Tracker Device" drop-down list. In this case, you can only use `Mouse` as a substitute, because it is (1) more convenient and does not affect the usability of the artifact, and (2) the calibration results will not be accurate when using VM.

#### Tracking

Click the `Tools -> Start Tracking` button on the menu bar. Then play something with the IDE just like you are programming. For example, you could move the mouse cursor, run the class, edit the code, close the file. Or use some fancy features of the IDE like go to the declaration, reformat the code, etc.

To test the "Add Labels" feature, you could right-click in the editor, and click `Add Label --> Fixed Bug x.y`. Then a notification should be shown in the bottom-right corner. The label will also be added to `ide_tracking.xml/<actions>` after the tracking is stopped.

You can test `Tools -> Pause Tracking` then `Tools -> Resume Tracking`, the data during the pause should be skipped.

After playing something for a while, click the `Tools -> Stop Tracking` button on the menu bar. After a refresh of the IDE (e.g. minimize and restore the IDE), the data will be exported to a folder in the pre-configured directory, i.e., the root directory of the project if you did not change it. The data directory name is the start tracking timestamp (e.g., `1703910153511`). You could see the exported data in such [structure](https://codegrits.github.io/CodeGRITS/data-format/#data-directory-structure).

Finally, browse the data files, especially the `ide_tracking.xml` (`<actions>` is perhaps the most important part), and `eye_tracking.xml`. They should successfully record your IDE interactions and eye gazes (i.e., mouse locations). See more details at [Data Format](https://codegrits.github.io/CodeGRITS/data-format/). This is the main results claimed in the paper.