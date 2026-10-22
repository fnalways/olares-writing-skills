# Example transformation

These excerpts illustrate editorial choices from QEMU Server and Pterodactyl documentation reviews. They are not complete deliverables or current product specifications. Verify app versions, UI labels, and settings before using them in a real guide.

## From porting notes to a useful task

Source notes:

> QEMU Server: four distributions covered in regression. Record machine ID and boot ID, resize CPU/RAM/disk, check marker-file persistence, test SSH and Clone isolation. Ubuntu uses ubuntu. Installation requires distribution, resources, and password. The Linux image initializes after app installation. Clone creates a fresh disk, not a copy. SSH and SFTP use the selected instance's connection details.

Editorial decisions:
- Use Ubuntu as the first server and Debian as the separate Clone example.
- Keep initialization readiness, credential sources, per-instance connection details, and disk/Clone limits.
- Put the test matrix, machine IDs, and coverage in the PR validation record.
- Keep Learning objectives even if the reviewed historical page omitted them.

Example English opening:

```markdown
# Run Linux servers with QEMU Server

QEMU Server runs Linux virtual machines on Olares. Use a server for command-line tools, development, or services, and manage it through SSH or a browser console.

This guide uses Ubuntu as the first server and Debian as a separate instance.

## Learning objectives

In this guide, you will learn how to:
- Install and initialize a Linux server.
- Connect to the server and transfer files.
- Create a separate server and adjust its resources.
```

Natural Chinese counterpart:

```markdown
# 使用 QEMU Server 运行 Linux 服务器

QEMU Server 可以在 Olares 上运行 Linux 虚拟机，用于运行命令行工具、搭建开发环境或托管服务。你可以通过 SSH 或浏览器控制台管理服务器。

本文先创建一台 Ubuntu 服务器，再创建一个独立的 Debian 实例。

## 学习目标

通过本文，你将学会：
- 安装并初始化 Linux 服务器。
- 连接服务器并传输文件。
- 创建独立服务器并调整资源。
```

The full guide still needs supported frontmatter, the actual steps, required navigation/gallery updates, and Chinese delivery according to the language workflow. Opening excerpts do not replace those deliverables.

## Keep the check that determines the next action

Test narration: record initialization time and verify guest startup across every supported distribution.

Tutorial instruction: open the app to view Linux initialization progress, wait for the documented ready state, then connect using the chosen distribution's account. Show where to find that state. An installed app does not by itself mean its guest OS is ready.

Do not invent a precise status label or typical duration from these notes.

## Replace a test fixture with a routine task

Test narration: run the Pterodactyl `playing` command once per minute, check the console response, then disable the test schedule.

Tutorial task: schedule the supported `save` command every 30 minutes to save the world. Explain where to create the schedule and enter its fields. Distinguish saving the current world from creating a separate restorable backup.

Use this task only when the app and game version support it. Do not imply that an editorial example has been executed or validates multiplayer capacity.
