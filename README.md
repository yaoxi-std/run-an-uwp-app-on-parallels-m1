# Run an UWP app via Parallels Desktop on m1

## 在M1上用PD运行UWP应用

If you are using Windows 10 (arm) on Parallels Desktop on you M1 Macbook, you may have found that such applications like Calculator and Microsoft-Store didn't run well. They flash back after you launched them.

如果你正在你的M1 macbook 上用PD运行Windows 10 (arm)，你会发现一些像计算器或是应用商店的程序无法运行。你一打开它们，它们就会闪退。

As Parallels Desktop said (you can find this on [parallels forums](https://forum.parallels.com/threads/microsoft-app-store.351930/)), "ARM32 Apps could not run via Parallels Desktop on M1". And I have also tried it. However, not all the UWP apps cannot run on M1. Some other apps like My-Phone runs well on it. After looking up the Task Manager, I found that these apps were all X86 UWP apps. These apps run well with X86 Emulator. So I got the point.

就像PD所说的那样（你可以在论坛上找到[parallels forums](https://forum.parallels.com/threads/microsoft-app-store.351930/)），“ARM32应用无法通过PD在M1上运行”。我也尝试过了。但是并非所有UWP都不能在M1上跑。一些像“你的手机”之类的应用运行的很流畅。我试图在任务管理器中查看这些应用，发现它们都是X86的UWP应用。这些应用都能通过X86仿真完美运行，所以我有了一个大胆的想法[滑稽]。

***

#### The following is the correct way to open UWP（打开UWP的正确方式）

（改天再翻译英文版了）（作者太懒

通过某种渠道（google），我了解到可以在[这个网站]()上查询到Windows商店中的应用。由此，我们可以通过搜索product id的方式来下载安装包

1. 在[microsoft.com](https://www.microsoft.com)搜索你想要的uwp应用，并在网址栏将product id复制下来

   例如：https://www.microsoft.com/zh-cn/p/windows-%e8%ae%a1%e7%ae%97%e5%99%a8/9wzdncrfhvn5?activetab=pivot:overviewtab （计算器）的product id就是上面的**9wzdncrfhvn5**

2. 打开[https://store.rg-adguard.net/](https://store.rg-adguard.net/)，在搜索框里填入product id（刚刚的那那段文字），将搜索框左边的菜单URL (link)改成ProductId，点右边的勾搜索

3. 稍等片刻，网页下方就会出现一堆的链接。随便找一个名字里包含"Calculator"的链接（最好是最底下的最新版），下载**后缀名为 .appxbundle**的文件

4. 这时不要着急，如果你已经安装过了这个app的arm32版本，先把它卸载掉（具体方法自己baidu或google）

5. 将下载好的.appxbundle文件后缀名改成.zip，然后解压，进入文件夹，你会发现一堆语言的文件包和一个名字带有"Win32"的后缀名为.appx的文件

6. 先直接点开名字带有"Win32"的.appx文件，系统会自动安装，然后再根据自己的语言（你是中文就点那个带有zh-hans或zh-cn的，如果没有语言文件就不安装语言文件）选择.appx文件点开安装（所以这一步一共要点开**两个**.appx包）

7. 如果提示不能安装，就打开powershell，输入 add-appxpackage 文件名.appx 会有红色的字提示你原因（大概率是缺少依赖文件），然后按照同样的步骤打开[https://store.rg-adguard.net/](https://store.rg-adguard.net/)，在搜索框里填入包的名称，将搜索框左边的菜单URL (link)**改成PackageFamilyName**，点右边的勾搜索，下载**相同架构（X86）**的依赖项按照同样的步骤安装好，最好再回过头来安装你需要的uwp应用

8. 然后你就会惊奇地发现，这个app可以打开了！而且跟我们平时在X86上运行的没有一点区别！


