**Lab 1 - Deploy host pools and session hosts by using the Azure portal
(Entra ID)**

**Lab dependencies**

- An Azure subscription you will be using in this lab.

- A Microsoft Entra user account with the Owner role in the Azure
  subscription you will be using in this lab and with the permissions
  sufficient to join devices to the Entra tenant associated with that
  Azure subscription.

**Estimated Time**

80 minutes

**Lab scenario**

You have a Microsoft Azure subscription. You need to deploy Azure
Virtual Desktop environment that uses Microsoft Entra joined session
hosts.

**Objectives**

After completing this lab, you will be able to:

- Deploy Microsoft Entra joined Azure Virtual Desktop session hosts

**Lab files**

- None

**Instructions**

**Exercise 1: Implement an Azure Virtual Desktop environment using
Microsoft Entra joined session hosts**

The main tasks for this exercise are as follows:

1.  Prepare the Azure subscription for deployment of an Azure Virtual
    Desktop host pool

2.  Deploy an Azure Virtual Desktop host pool

3.  Create an Azure Virtual Desktop application group

4.  Create an Azure Virtual Desktop workspace

5.  Grant access to Azure Virtual Desktop host pools

**Task 1: Create Desktop and Remote Application Groups**

Step 1: Create a New Group for AVD-DAG

1.  In the Azure portal, use the search bar to find and
    select [**Microsoft Entra ID**](urn:gd:lg:a:send-vm-keys).

2.  In the **Overview** page of the Microsoft Entra tenant linked to
    your subscription, navigate to the **Manage** section in the
    left-hand menu and select **Groups**.

3.  On the **Groups** page, click **New group** and enter the group
    name [**AVD-DAG-XXXXXX**](urn:gd:lg:a:send-vm-keys) (replace **XXXXXX** with
    a unique identifier).

4.  Select **Members**, and add the User1- and User2- account to the
    group **AVD-DAG-XXXXXX**.

5.  Click **Create**.

Step 2: Create a New Group for AVD-RemoteApp

1.  In the Azure portal, search for and select [**Microsoft Entra
    ID**](urn:gd:lg:a:send-vm-keys) again.

2.  On the **Overview** page of your Microsoft Entra tenant, under
    the **Manage** section, select **Groups**.

3.  On the **Groups** page, click **New group** and enter the group
    name [**AVD-RemoteApp-XXXXXX**](urn:gd:lg:a:send-vm-keys) (replace **XXXXXX** with
    a unique identifier).

4.  Select **Members**, and add the User1- and User2- account to the
    group **AVD-RemoteApp-XXXXXX**.

5.  Click **Create**.

**Task 2: Prepare the Azure subscription for deployment of an Azure
Virtual Desktop host pool**

1.  From the lab computer, start a web browser, navigate to the Azure
    portal at [https://portal.azure.com](https://portal.azure.com/) and
    sign in by providing the credentials of a user account with the
    Owner role in the subscription you will be using in this lab.

**Note**: Use the credentials of the User1- account listed on the
Resources tab on the right side of the lab session window.

2.  In the Azure portal, start a PowerShell session in the Azure Cloud
    Shell.

**Note**: If prompted, in the **Getting started** pane, in
the **Subscription** drop-down list, select the name of the Azure
subscription you are using in this lab and then select **Apply**.

3.  In the PowerShell session in the Azure Cloud Shell pane, run the
    following command to register
    the **Microsoft.DesktopVirtualization** resource provider:

Register-AzResourceProvider -ProviderNamespace
Microsoft.DesktopVirtualization

**Note**: Do not wait for the registration to complete. This might take
a couple of minutes.

4.  Close the Cloud Shell pane.

5.  In the web browser displaying the Azure portal, search for and
    select **Virtual networks** and, on the **Virtual networks** page,
    select **Create +**

6.  On the **Basics** tab of the **Create virtual network** page,
    specify the following settings and select **Next**:

[TABLE]

7.  On the **Security** tab, accept the default settings and
    select **Next**.

8.  On the **IP addresses** tab, apply the following settings (modify
    the default if needed):

[TABLE]

9.  Select the edit (pencil) icon next to the **default** subnet entry,
    in the **Edit** pane, specify the following settings (leave others
    with their existing values) and select **Save**:

[TABLE]

10. Back on the **IP addresses** tab, select **Review + create** and
    then, on the **Review + create** tab, select **Create**.

**Note**: Do not wait for the provisioning process to complete. This
typically takes less than 1 minute.

11. In the web browser displaying the Azure portal, search for and
    select **Microsoft Entra ID**.

12. On the **Overview** page of the Microsoft Entra tenant associated
    with your subscription, in the **Manage** section of the vertical
    navigation menu, select **Users**.

13. On the **Users** page, in the **Search** text box, enter the name of
    the User1- account listed on the Resources tab on the right side of
    the lab session window.

14. In the list of results of the search, select the user account entry
    with the matching name.

15. On the page displaying the properties of the user account, in
    the **Manage** section of the vertical navigation menu,
    select **Groups**.

16. On the **Groups** page, record the name of the group starting
    with **AVD-DAG** prefix (you will need it later in this lab).

17. Navigate back to the **Users** page, in the **Search** text box,
    enter the name of the User2- account listed on the Resources tab on
    the right side of the lab session window.

18. In the list of results of the search, select the user account entry
    with the matching name.

19. On the page displaying the properties of the user account, in
    the **Manage** section of the vertical navigation menu,
    select **Groups**.

20. On the **Groups** page, record the name of the group starting
    with **AVD-RemoteApp** prefix (you will need it later in this lab).

**Task 3: Deploy an Azure Virtual Desktop host pool**

1.  From the lab computer, in the web browser displaying the Azure
    portal, search for and select **Azure Virtual Desktop**, on
    the **Azure Virtual Desktop** page, in the **Manage** section of the
    vertical navigation menu, select **Host pools** and, on the **Azure
    Virtual Desktop | Host pools** page, select **+ Create**.

2.  On the **Basics** tab of the **Create a host pool** page, specify
    the following settings and select **Next: Session hosts \>** (leave
    other settings with their default values):

[TABLE]

3.  **Note**: When using the Breadth-first load balancing algorithm, the
    max session limit parameter is optional.

4.  On the **Session hosts** tab of the **Create a host pool** page,
    specify the following settings and select **Next: Workspace
    \>** (leave other settings with their default values):

**Note**: When setting the **Name prefix** value, switch to the
Resources tab on the right side of the lab session window and identify
the string of characters between *User1-* and the *@* character. Use
this string to replace the *random* placeholder.

[TABLE]

**Note**: The password should be at least 12 characters in length and
consist of a combination of lower-case characters, upper-case
characters, digits, and special characters. For details, refer to the
information about [the password requirements when creating an Azure
VM](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm-).

5.  On the **Workspace** tab of the **Create a host pool** page, confirm
    the following setting and select **Review + create**:

[TABLE]

6.  On the **Review + create** tab of the **Create a host pool** page,
    select **Create**.

**Note**: Wait for the deployment to complete. This might take about 20
minutes.

**Task 4: Create an Azure Virtual Desktop application group**

1.  From the lab computer, in the web browser displaying the Azure
    portal, search for and select **Azure Virtual Desktop** and, on
    the **Azure Virtual Desktop** page, select **Application groups**.

2.  On the **Azure Virtual Desktop | Application groups** page, note the
    existing, auto-generated **az140-21-hp1-DAG** desktop application
    group, and select it.

3.  On the **az140-21-hp1-DAG** page, in the **Manage** section of the
    vertical navigation menu, select **Assignments**.

4.  On the **az140-21-hp1-DAG | Assignments** page, select **+ Add**.

5.  On the **Select Microsoft Entra users or user groups** page,
    select **Groups**, in the search box, type the full name of
    the **AVD-DAG** group you identified in the first task of this
    exercise, select the checkbox next to the group name, and
    click **Select**.

6.  Navigate back to the **Azure Virtual Desktop | Application
    groups** page, select **+ Create**.

7.  On the **Basics** tab of the **Create an application group** page,
    specify the following settings and select **Next: Applications \>**:

[TABLE]

8.  On the **Applications** tab of the **Create an application
    group** page, select **+ Add applications**.

9.  On the **Add application** page, specify the following settings and
    select **Review + add**, then select **Add**:

[TABLE]

10. Back on the **Applications** tab of the **Create an application
    group** page, select **+ Add applications**.

11. On the **Add application** page, specify the following settings and
    select **Review + add**, then select **Add**:

[TABLE]

12. Back on the **Applications** tab of the **Create an application
    group** page, select **+ Add applications**.

13. On the **Add application** page, specify the following settings and
    select **Review + add**, then select **Add**:

[TABLE]

14. Back on the **Applications** tab of the **Create an application
    group** page, select **Next: Assignments \>**.

15. On the **Assignments** tab of the **Create an application
    group** page, select **+ Add Microsoft Entra users or user groups**.

16. On the **Select Microsoft Entra users or user groups** page,
    select **Groups**, type the full name of the **AVD-RemoteApp** group
    you identified in the first task of this exercise, select the
    checkbox next to the group name, and click **Select**.

17. Back on the **Assignments** tab of the **Create an application
    group** page, select **Next: Workspace \>**.

18. On the **Workspace** tab of the **Create a workspace** page, specify
    the following setting and select **Review + create**:

[TABLE]

19. On the **Review + create** tab of the **Create an application
    group** page, select **Create**.

**Note**: Wait for the Application Group to be created. This should take
less than 1 minute.

**Note**: Next you will create an application group based on file path
as the application source.

20. In the web browser displaying the Azure portal, search for and
    select **Azure Virtual Desktop** and, on the **Azure Virtual
    Desktop** page, select **Application groups**.

21. On the **Azure Virtual Desktop | Application groups** page,
    select **+ Create**.

22. On the **Basics** tab of the **Create an application group** page,
    specify the following settings and select **Next: Applications \>**:

[TABLE]

23. On the **Applications** tab of the **Create an application
    group** page, select **+ Add applications**.

24. On the **Add application** page, on the **Basics** tab, specify the
    following settings and select **Next**:

[TABLE]

25. On the **Icon** tab, specify the following settings and
    select **Review + add**, then select **Add**:

[TABLE]

26. Back on the **Applications** tab of the **Create an application
    group** page, select **Next: Assignments \>**.

27. On the **Assignments** tab of the **Create an application
    group** page, select **+ Add Microsoft Entra users or user groups**.

28. On the **Select Microsoft Entra users or user groups** page,
    select **Groups**, type the full name of the **AVD-RemoteApp** group
    you identified in the first task of this exercise, select the
    checkbox next to the group name, and click **Select**.

29. Back on the **Assignments** tab of the **Create an application
    group** page, select **Next: Workspace \>**.

30. On the **Workspace** tab of the **Create a workspace** page, specify
    the following setting and select **Review + create**:

[TABLE]

31. On the **Review + create** tab of the **Create an application
    group** page, select **Create**.

**Note**: Wait for the Application Group to be created. This should take
less than 1 minute.

**Task 5: Create an Azure Virtual Desktop workspace**

1.  From the lab computer, in the web browser displaying the Azure
    portal, search for and select **Azure Virtual Desktop** and, on
    the **Azure Virtual Desktop** page, select **Workspaces**.

2.  On the **Azure Virtual Desktop | Workspaces** page, select **+
    Create**.

3.  On the **Basics** tab of the **Create a workspace** page, specify
    the following settings and select **Next: Application groups \>**:

[TABLE]

4.  On the **Application groups** tab of the **Create a
    workspace** page, specify the following settings:

[TABLE]

5.  On the **Workspace** tab of the **Create a workspace** page,
    select **+ Register application groups**.

6.  On the **Add application groups** page, select the plus sign next to
    the **az140-21-hp1-DAG**, **az140-21-hp1-Office365-RAG**,
    and **az140-21-hp1-Utilities-RAG** entries and click **Select**.

7.  Back on the **Application groups** tab of the **Create a
    workspace** page, select **Review + create**.

8.  On the **Review + create** tab of the **Create a workspace** page,
    select **Create**.

**Task 6: Grant access to Azure Virtual Desktop host pools**

**Note**: When using Microsoft Entra joined session hosts, you need to
assign to Azure Virtual Desktop users and administrators appropriate
Azure role-based access control (RBAC) roles. In particular,
the *Virtual Machine User Login* role is required to sign in to session
hosts and the *Virtual Machine Administrator Login* role is required for
the local administrative privileges.

1.  From the lab computer, in the web browser displaying the Azure
    portal, search for and select **Resource groups** and, on
    the **Resource groups** page, select **az140-21e-RG**.

2.  On the **az140-21e-RG** page, in the vertical navigation menu,
    select **Access control (IAM)**.

3.  On the **az140-21e-RG|Access control (IAM)** page, select **+
    Add** and, in the drop-down menu, select **Add role assignment**.

4.  On the **Role** tab of the **Add role assignment** page, ensure that
    the **Job function roles** tab is selected, in the search textbox,
    enter **Virtual Machine User Login**, in the list of results,
    select **Virtual Machine User Login**, and then select **Next**.

5.  On the **Members** tab of the **Add role assignment** page, ensure
    that the **User, group, or service principal** option is selected,
    click **+ Select members**, in the **Select members** pane, locate
    the **AVD-RemoteApp** group you identified in the first task of this
    exercise, and click **Select**.

6.  Back on the **Members** tab of the **Add role assignment** page,
    select **Next**.

7.  On the **Assignment type** tab of the **Add role assignment** page,
    set the **Assignment type** to **Active** and then select **Review +
    assign**.

8.  On the **Review + assign** tab of the **Add role assignment** page,
    select **Review + assign**.

9.  Back on the **az140-21e-RG|Access control (IAM)** page, select **+
    Add** and, in the drop-down menu, select **Add role assignment**.

10. On the **Role** tab of the **Add role assignment** page, ensure that
    the **Job function roles** tab is selected, in the search textbox,
    enter **Virtual Machine Administrator Login**, in the list of
    results, select **Virtual Machine Administrator Login**, and then
    select **Next**.

11. On the **Members** tab of the **Add role assignment** page, ensure
    that the **User, group, or service principal** option is selected,
    click **+ Select members**, in the **Select members** pane, locate
    the **AVD-DAG** group you identified in the first task of this
    exercise, and click **Select**.

12. Back on the **Members** tab of the **Add role assignment** page, set
    the **Assignment type** to **Active**, select **Review +
    assign** and then select **Review + assign** again.
