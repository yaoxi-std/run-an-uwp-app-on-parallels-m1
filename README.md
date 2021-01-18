# 在M1上用PD运行UWP应用

## Run UWP apps via PD on M1

如果你正在你的M1 macbook 上用PD运行Windows 10 (arm)，你会发现一些像计算器或是应用商店的程序无法运行。你一打开它们，它们就会闪退。

If you are using Windows 10 (arm) on Parallels Desktop on you M1 Macbook, you may have found that such applications like Calculator and Microsoft-Store didn't run well. They flash back after you launched them.

就像PD所说的那样（你可以在论坛上找到[parallels forums](https://forum.parallels.com/threads/microsoft-app-store.351930/)），“ARM32应用无法通过PD在M1上运行”。我也尝试过了。但是并非所有UWP都不能在M1上跑。一些像“你的手机”之类的应用运行的很流畅。我试图在任务管理器中查看这些应用，发现它们都是X86的UWP应用。这些应用都能通过X86仿真完美运行，所以我有了一个大胆的想法[滑稽]。

As Parallels Desktop said (you can find this on [parallels forums](https://forum.parallels.com/threads/microsoft-app-store.351930/)), "ARM32 Apps could not run via Parallels Desktop on M1". And I have also tried it. However, not all the UWP apps cannot run on M1. Some other apps like My-Phone runs well on it. After looking up the Task Manager, I found that these apps were all X86 UWP apps. These apps run well with X86 Emulator. So I got the point.

***

#### 打开UWP的正确方式 (The right way to open an UWP app)

**此方法只适用于能在Microsoft Store上搜索到的UWP应用。（我一个初二学生自己摸索出来的方法）**

**This method only works on UWP Apps which can be found on Microsoft Store (I am a junior 2 student to explore this method).**

通过某种渠道（google），我了解到可以在[这个网站](https://store.rg-adguard.net/)上查询到Windows商店中的应用。因此，我们可以通过搜索网址的方式来下载安装包。

In some ways (google) , I found that it is possible to query Apps in Microsoft Store on [this website](https://store.rg-adguard.net/). By this, we can download the installation files by searching URLs.

1. 在[microsoft.com](https://www.microsoft.com)搜索你想要的UWP应用，并在网址栏将网址复制下来。

   例如：https://www.microsoft.com/zh-cn/p/windows-%e8%ae%a1%e7%ae%97%e5%99%a8/9wzdncrfhvn5（计算器）

   Search the UWP apps you want on [microsoft.com](https://www.microsoft.com), and copy the URL.

   e.g. https://www.microsoft.com/zh-cn/p/windows-%e8%ae%a1%e7%ae%97%e5%99%a8/9wzdncrfhvn5 (Calculator)

2. 打开[https://store.rg-adguard.net/](https://store.rg-adguard.net/) 并黏贴网址，点右边的搜索。

   Open [https://store.rg-adguard.net/](https://store.rg-adguard.net/) and paste the URL, then press the button on your right.

3. 稍等片刻，网页下方就会出现一堆的链接。下载后缀名为 **.appxbundle**的最新版本的文件。（请注意看好文件名）

   Wait a minute. There will be some URLs below. Download the latest version with suffix **.appxbundle**. (pay attention to the filenames)

4. 这时不要着急，如果你已经安装过了这个应用的ARM32版本，先把它卸载掉。（具体方法自己百度或谷歌）

   Be patient. If you have already installed an ARM32 version, please uninstall it first. (google or baidu by your self)

5. 将下载好的.appxbundle文件后缀名改成.zip，然后解压，进入文件夹，你会发现一堆语言的文件包和一个名字带有"Win32"的后缀名为.appx的文件。

   Change the suffix of the downloaded file into .zip , then unzip it, cd into it, you will find plenty of language files and an .appx file with substring "Win32" or "X86".

6. 以管理员身份运行Powershell（如果Powershell闪退，请先以管理员身份打开CMD，并输入powershell），然后CD到刚刚的文件夹，输入以下代码：

   Open Powershell with Administration (If you Powershell flashes back, you can open CMD with Administration and type 'powershell'), then cd into the above directory. Input the following code:

```powershell
add-appxpackage *win32*    # Or 'add-appxpackage *x86*' if the substring of the .appx file is 'x86'
add-appxpackage *scale*    # Install the scales
add-appxpackage *zh-hans*  # Install language packages. You can change it into other languages like *en-us*
```

7. 如果出现红字，请检查该应用的依赖文件。 在 [https://store.rg-adguard.net/](https://store.rg-adguard.net/) 上查找依赖文件并下载安装。

   If some red words appear, please check the dependencies of this app. Search the dependency packages on [https://store.rg-adguard.net/](https://store.rg-adguard.net/) and download and install it first.

8. 然后你就会惊奇地发现，这个app可以完美运行了！享受吧！

   In the end, you will see these UWP apps work well on you computer. Enjoy it!



你还可以在[B站](https://www.bilibili.com/video/BV1hp4y1x79y)上看到我的操作方法的视频（只不过用了另一种搜索包文件的方法）。

You can also see the operations on [Bilibili](https://www.bilibili.com/video/BV1hp4y1x79y) (it used another way to search the package files).
