# Installing and setting up the Eclipse IDE for running simulations with OpenTrafficSim
 
The following information has been retrieved from https://opentrafficsim.org/old/index.php/setting-up-eclipse
 
## Before you start
Consider printing this document so you can make notes on it and have your entire screen devoted to installing the software. If you find errors or problems, please fix this document please raise an issue. 

## Download and install Java 13 Development Kit (OpenJDK 13)
(This guide assumes the open version 13, but any later version is applicable and advisable, and the registered version also applies)

Download the **Java SE 13 JDK** (make sure you do not get just the **JRE**). Oracle does not provide installations files for OpenJDK, but these can be downloaded from https://adoptopenjdk.net/. Agree to any licenses.

## Installing Eclipse
Download Eclipse from https://www.eclipse.org/downloads/ and install it as required for your operating system. During the installation you are advised to select the Enterprise version for installation. Whatever you choose, make sure Maven is included.

## Configuring Eclipse
The first time you run eclipse it will ask you to select a workspace. Select a place on a disk that has enough space (several GB) and make sure that there are **NO SPACES** in the path leading up to your workspace. Check the check box "Use this as the default and do not ask again", then click OK. On first run you'll now get to the "Welcome to Eclipse" screen. Along the the right of that screen is a button "Workbench". Click that to get to the Java perspective. (Perspective is Eclipse-speak for a window layout.) The Java perspective is used for writing Java code. The name of all recently used perspectives are shown as buttons in the top right of the window. Click on that button to change to that perspective. Eclipse can be intimidating at first.

## Making sure Eclipse uses the previously installed JDK
In the main menu click **Window**, then **Preferences**. Expand **Java**, click on **Installed JREs**. It will likely show the installed JDK.

If not, click **Add ...**, select **Standard VM**, click **Next**. Click **Directory ...**, navigate to the directory with the JDK. Select this directory (not any of its sub-directories). The box **JRE name** should now show the name and version of the JDK. Click **Finish**. You'll get back to the Installed JREs overview. Check the check box in front of the JDK, then click OK.

Right-click in the **Package Explorer** sub-window (if you can't see this, go to **Window, Show View, Other...**, and select **Java > Package Explorer**). In the context menu click **New, (Other...** if required), then **Java Project**. Check that in the JRE outline, the box after **Use a project specific JRE:** shows the installed JDK. Click **Cancel** (we do not want to create a new project).

## Installing additional Eclipse functionality
### Install Subclipse SVN support
In the main menu click **Help**, then **Install New Software....** Click the **Add ...** button. In the **Name** box type Subclipse, in the Location box type http://subclipse.tigris.org/update_1.10.x

After a few seconds **Subclipse** should appear under Name.  Click the check box in front of it and click Next. In the **Install Details** window click **Next**. In the **Review Licenses** window click **I accept the terms of the license agreement**, then click **Finish**. You may get a warning about unsigned content. Tell eclipse to continue by clicking **Install anyway**. Restart eclipse when it asks you to do so.

### Install ObjectAid Class Diagram (optional)

In the main menu click **Help**, then **Install New Software....** Click the **Add ...** button. In the Name box type **ObjectAid**, in the Location box type http://objectaid.com/update/current

If it does not work, look at http://www.objectaid.com for installation help.

After a few seconds the **ObjectAid UML Explorer** will apear under **Name**. Expand it and check the check box in front of **ObjectAid Class Diagram** and click **Next**. In the **Install Details** window click **Next**. In the **Review Licenses** window click **I accept the terms of the license agreement**, then click **Finish**. You may get a warning about unsigned content. Tell eclipse to continue by clicking **Install anyway**. Restart eclipse when it asks you to do so.

## Retrieving the OpenTrafficSim project from the SVN repository
In the Java perspective right-click in the **Package Explorer** sub-window and select **Import....** Expand **SVN**, then highlight on **Checkout Projects from SVN**. Click **Next**. In the Checkout from SVN window click **Next**. Type https://svn.tbm.tudelft.nl/OTS in the Url box and click **Next**. After a few seconds a tree view of the repository should appear. Select **trunk/ots-build-tools** and click **Next** (do not click **Finish** at this point). In the Checkout from SVN window select **Check out as a project in the workspace** then click **Finish**.

### Install the checkstyle plugin
In the main Eclipse menu click **Help**, then **Eclipse Marketplace...**, In the **Eclipse Marketplace** popup type _checkstyle_ in the **Find**: box, then type the Enter key. After a few seconds a list should appear containing **Checkstyle Plug-in 8.26.0** (the version number may be higher). Click the **Install** button for that entry. Agree to the license agreement and click **Install anyway** on the warning dialog about unsigned content. Let Eclipse restart when it suggest you to do so.

In the Eclipse main menu click **Window**, then **Preferences**, then select **Checkstyle**. Click **New ...**, then select **Project Relative Configuration** as **Type:**. then click **Browse ...** and navigate to **ots-buld-tools/src/main/resources/development** and select **dsol-checks.xml** and click the **OK** button. Back in the Check Configuration Properties window type _dsol-checks_ in the **Name:** field, then click the **OK** button. Back in the **Preferences** window select the **dsol-checks** configuration and click on the **Set as Default** button. Click **Apply and Close**.

### Import remaining java projects
Repeat the importing steps done for **ots-build-tools** but regarding **ots, ots-base, ots-core, ots-kpi, ots-road, ots-animation, ots-draw, ots-swing, ots-web, ots-parser-osm, ots-parser-xml, ots-xsd, ots-trafficcontrol** and **ots-demo** (you can now select the repository from the list; you don't have to re-type the Url).

### Checking that it works
Restart eclipse. At this time eclipse is probably confused due to all the changes to the files. In the eclipse main menu click **Project**, then click **Clean...**, in the Clean dialog click **OK**. In the Package Explorer sub-window right-click on ots, click on Refresh.

If at this point errors (red-crosses in the Package Explorer) remain, do the following. Go to **Windows**, then **Preferences**. Expand **Java** and click on **Compiler**. For **Compiler cimpliant level:** select 1.8.

Expand **ots-demo**, then expand **src/main/java**, then expand **org.opentrafficsim.demo** and open **CircularRoadSwing** by double-clicking on it. Right-click on **CircularRoadSwing** and select **Run As**, then **Java Application**. (If one of these items is not present in the menu, something is not correctly configured.)

If everything works a small window appears with one button labeled OK. Click it and a series of contour graph windows should appear. After a few seconds the contents of these windows will be updated showing contour graphs of a traffic jam.

### How to commit changes
In the sections above the code was checked out anonymously. This is possible because the source code repository is publicly readable.

In order to commit changes you will need to be registered as a user on https://svn.tbm.tudelft.nl/OTS. Contact Peter Knoppers or Alexander Verbraeck to get registered. On your first commit eclipse will ask you for your credentials and offer to save them.

Once you are registered the commit procedure is as follows:

Right-click on the top level entry in the Package Explorer (your source code is likely in ots-core, or ots-demo). In the context menu select **Team**, then **Synchronize with Repository**.

The first time you do this you'll get the **Confirm Open Perspective** dialog. Check the **Remember my decision** check box and click **Yes**. This opens the **Team Synchronizing** perspective. In the top-left sub-window is a tree view with your uncommited changes and any files updated on the server that you should update. If there are pending updates, you should update first. Then go back to the Java Perspective and check that everything (still) works and fix any problems. (To go back to the Java Perspective click the **Java** button in the top right of the eclipse main window.) If a file is changed on the SVN server as well as locally, you may have to resolve any conflicts before you can commit.

When there are no conflicts and no pending updates you should commit your changes. Right-click on the entry in the SVN sub-window and select **Commit...** from the context menu. In the to left box in the Commit window enter a short description of your changes, then click the **OK** button. If you have several unrelated changes to commit, select them one by one in the tree view and give each one a suitable description.

Commits in subversion are atomic; they either succeed completely or fail completely (leaving no trace in the repository); it is not possible that a commit succeeds partially. The most common reasons for failing a commit are conflicting changes and out of memory problems on the server.

## Setting the eclipse code preferences
These are stored in the ots-build-tools tree. To activate them select in the main menu **File**, then click **Import**, expand **General**, select **Preferences**, click **Next**, click **Browse**. navigate to your workspace folder and in that folder to **ots-build-tools**, then **src**, then **main**, then **resources**, then **development** and select **eclipse43-ots.epf**. Click **Open**. Check the check box **Import all**, click **Finish**.

The default javadoc for a class will now contain all main contributers. This means you will have to delete all others each time you create a new class. You can edit file **eclipse43-ots.epf** to contain only yourself (do not commit that change).

To re-format the file you are currently editing type ctrl-shift-F. To re-format a group of source code files select the root of the group in the **Package Explorer** sub-window and type ctrl-shift-F. To undo an accidental re-format type ctrl-Z.)

## Installing and using FindBugs (optional)
FindBugs is a tool available as plug-in for Eclipse that you can run to find (potential) bugs in java code.

### Installing FindBugs
In Eclipse, go to **Help** and **Install new software…**. In the new window type the following in the **Work with** field: http://findbugs.cs.umd.edu/eclipse/. Click **Add**.

In a new window, give a name in the **Name** field, e.g. **FindBugs**. Click **Ok**. Back in the previous window, check **FindBugs** in the list and click **Next** twice. Accept the terms and conditions with the radio-button and click **Finish**. You might get a security warning for unsigned content, accept with **Ok**. Eclipse needs to restart which you can do by clicking **Yes**.

### Using FindBugs
Right-click on a project, package or java-file in the Package Explorer and go to the **Find Bugs** submenu and click **Find Bugs**. FindBugs will find bugs in the selected code and show the number of bugs found in the Package Explorer by appending e.g. **(5)** to the name in case of 5 bugs in the file/package/project. You can find individual bugs through markers shown to the left of a line of code where the bug is found. You can hover the mouse over the marker to get a message, or right-click and select **Show Bug Info**.

If you believe that the ‘bug’ is not a problem (FindBugs is not always correct, consider the found ‘bugs’ as warnings), you may suppress it. To suppress, add the following annotation to the method.
```
@SuppressFBWarnings("ERROR_PATTERN")
public myMethod(...
```
The **error pattern** can be found in the bug info and will look like the following example: RV_RETURN_VALUE_IGNORED. Note that the FindBugs warning is suppressed for the entire method, so, FindBugs will not warn you for this specific kind of bug throughout the method.

To remove all bug markers, right-click in the Package Explorer and go to the **Find Bugs** submenu and click **Clear Bug Markers**.
