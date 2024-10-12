---
layout: post
title: Check and Set Java JDK Versions on macOS
---

**Understanding Java and JDK**

Before diving into the commands, let's clarify:

* **Java:** A programming language used to create software applications.
* **JDK (Java Development Kit):** A toolkit that includes the Java Runtime Environment (JRE), compiler, debugger, and other tools needed to develop Java applications.

**Checking the Current JDK Version**

1.  **Open Terminal:** Use the Spotlight search (Command + Space) or navigate to Applications \> Utilities \> Terminal.
2.  **Execute the Command:** Type the following command and press Enter:
    ```bash
    java -version
    ```
    This will display the installed Java version. If no output appears, it means Java is not installed.

**Installing a Specific JDK**

If you need to install a different JDK (e.g., for a specific project or environment), follow these steps:

1.  **Download the JDK:** Visit the Oracle website ([https://www.oracle.com/java/technologies/downloads/](https://www.google.com/url?sa=E&source=gmail&q=https://www.oracle.com/java/technologies/downloads/)) and download the desired JDK for macOS.
2.  **Extract the Archive:** Double-click the downloaded DMG file and drag the JDK folder to the `/Library/Java/JavaVirtualMachines` directory.
3.  **Update Environment Variables:** Open Terminal and execute the following command to update the environment variables:
    ```bash
    sudo nano /etc/profile
    ```
    Add the following line to the end of the file, replacing `/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home` with the actual path to your JDK:
    ```bash
    export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home"
    ```
    Save the file (Command + X, then Y) and close the Terminal.
4.  **Reload Environment Variables:** Open a new Terminal window or execute the following command in the existing one:
    ```bash
    source /etc/profile
    ```

**Setting a Default JDK**

To set a specific JDK as the default, use the following command, replacing `/Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home` with the desired JDK path:

```bash
sudo defaults write /Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home/bin/java -currentVersion -XstartOnFirstThread
```

**Verifying the Default JDK**

To check the current default JDK, execute the following command:

```bash
/usr/libexec/java_home -V
```

**Additional Tips**

* **Homebrew:** If you use Homebrew, you can install and manage JDKs using the `brew` command. For example, to install JDK 11:
  ```bash
  brew install openjdk@11
  ```
* **Multiple JDKs:** You can have multiple JDKs installed and switch between them using the `JAVA_HOME` environment variable or tools like `jenv` or `sdkman`.

By following these steps, you can effectively manage Java JDK versions on your macOS system.

