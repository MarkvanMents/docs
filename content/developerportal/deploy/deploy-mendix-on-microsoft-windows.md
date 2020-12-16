# Microsoft Windows
1 | xas | `^(xas/)(.*)` | `http://localhost:8080/{R:1}{R:2}`
2 | ws | `^(ws/)(.*)` | `http://localhost:8080/{R:1}{R:2}`
3 | ws-doc | `^(ws-doc/)(.*)` | `http://localhost:8080/{R:1}{R:2}`
4 | ws-file | `^(file)(.*)` | `http://localhost:8080/{R:1}{R:2}`
5 | link | `^(link/)(.*)` | `http://localhost:8080/{R:1}{R:2}`
6 | rest | `^(rest/)(.*)` | `http://localhost:8080/{R:1}{R:2}`
7 | rest-doc | `^(rest-doc/)(.*)` | `http://localhost:8080/{R:1}{R:2}`

Follow the instructions below and replace *[Name]* with the name of the rule in the table above, *[Pattern]* with the regular expression pattern, and *[Rewrite URL]* with the Rewrite URL. Note that some patterns contain a trailing slash, `/`, when they need to point to an exact path (for example, `/ws-doc/mydoc/1234`).

1. Open the IIS Manager and navigate to the website you want to manage.

2. In the **Features View**, double-click **URL Rewrite**.

3. In the **Actions** pane on the right side of the screen, click **Add rule(s)…** to add a new rewrite rule.

4. In the **Inbound Rules** field, enter *localhost:8080*, then click **OK**.

5. Select **ReverseProxyInboundRule1** in **Features View**.

6. In the **Actions** pane on the right side of the screen, click **Rename**.

7. Rename **ReverseProxyInboundRule1** to *[Name]*.

8. Double-click **[Name]** in **Features View** to change the properties of your rule.

9. In the **Pattern field** enter `[Pattern]`.

10. In the **Rewrite URL** field, enter `[Rewrite URL]` (in the rules above this is always `http://localhost:8080/{R:1}{R:2}`).

11. Click **Apply**.

12. Click **Back to Rules**.

13. Repeat from step 3 to add all the required rules.

You can also add additional request handlers in the same way. However you must ensure that they come *after* the rule *add x-forwarded-proto header*, described below.


#### 5.4.2 Rule *add x-forwarded-proto header*

This is required to ensure that you can access the Swagger documentation of your published REST services. It has to be the first rule; it is described last to ensure that it is moved to the top and that additional rules are not placed above it accidentally.

1. Click **View Server Variables**

2. Check if server variable **HTTP_X_FORWARDED_PROTO** is listed. If it is, skip to step 7.

3. In the **Action** page, click **Add** to add the server variable.

4. Enter the **Server variable name** *HTTP_X_FORWARDED_PROTO*.

5. Click **OK**.

6. Click **Back to Rules**

7. Click **Add rule(s)…**.

8. Click **Blank Rule**.

9. Set the **Name** to *add x-forwarded-proto header*.

10.	In the **Match URL** section, set **Requested URL** to *Matches the Pattern*.

11. Set **Using** to *Regular Expressions*.

12. Set the **pattern** to `.*`.

13. Set **Ignore Case** to *true* (checked).

14.	In the **Server Variables** section, click **Add**.

15.	Select Server variable name **HTTP_X_FORWARDED_PROTO**

16. Set **Value** to *https*.

17. Click **OK**.

18.	In the **Action** section, select **None**.

19. Set **Stop processing of subsequent rules** to *false* (unchecked).

20.	Click **Apply** in the **Action** pane to save the rule.

21. Click **Back to Rules**.

22. Select the newly created *add x-forwarded-proto header* rule and use the **Move Up** button in the Action pane to move the rule to the top of the list.

### 5.5 Disabling the Client Cache

In the application directory under **Project/Web**, you will find the `web.config` file that contains the MS IIS configuration for the application. You should add the following code to this file, between the `<system.webServer></system.webServer>` tags.
:

```xml
<staticContent>
    <clientCache cacheControlMode="DisableCache" />
</staticContent>
```

Afterwards, the contents of this file will be similar to the following example:

**web.config**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="add x-forwarded-proto header">
                    <match url=".*" />
                    <conditions logicalGrouping="MatchAll" trackAllCaptures="false" />  <serverVariables>
                        <set name="HTTP_X_FORWARDED_PROTO" value="https" />
                    </serverVariables>
                    <action type="None" />
                </rule>
                <rule name="xas" stopProcessing="true">
                    <match url="^(xas/)(.*)" />
                    <action type="Rewrite" url="http://localhost:8080/{R:1}{R:2}" />
                </rule>
                <rule name="ws" stopProcessing="true">
                    <match url="^(ws/)(.*)" />
                    <action type="Rewrite" url="http://localhost:8080/{R:1}{R:2}" />
                </rule>
                <rule name="ws-doc" stopProcessing="true">
                    <match url="^(ws-doc/)(.*)" />
                    <action type="Rewrite" url="http://localhost:8080/{R:1}{R:2}" />
                </rule>
                <rule name="ws-file" stopProcessing="true">
                    <match url="^(file)(.*)" />
                    <action type="Rewrite" url="http://localhost:8080/{R:1}{R:2}" />
                </rule>
                <rule name="link" stopProcessing="true">
                    <match url="^(link/)(.*)" />
                    <action type="Rewrite" url="http://localhost:8080/{R:1}{R:2}" />
                </rule>
            </rules>
        </rewrite>
        <staticContent>
            <mimeMap fileExtension=".mxf" mimeType="text/xml" />
            <clientCache cacheControlMode="DisableCache" />
        </staticContent>
    </system.webServer>
</configuration>
```

## 6 Preserving the Host Header

To make sure the correct application root URL is used within your web services, you must make sure the host header contains the original host header from the client request. To make sure the host header is preserved, follow these steps.

1. Click **Start**, and then click **All Programs**.

2. Click **Accessories**, and then click **Command Prompt**.

3. Execute the following command from the command prompt:

    ```batchfile
    cd %windir%\system32\inetsrv
    ```

4. Enter:

    ```batchfile
    appcmd.exe set config -section:system.webServer/proxy /preserveHostHeader:"True" /commit:apphost
    ```

## 7 Troubleshooting

When configuring IIS it can seem like you have done everything right but it just doesn't seem to work. A guide to troubleshooting IIS is available here: [Troubleshooting IIS](troubleshooting-iis).

## 8 Read More

* [On-Premises](on-premises-design)
