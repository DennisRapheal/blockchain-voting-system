![2021-06-16 (12)](https://user-images.githubusercontent.com/82329310/122496997-47142c00-d01f-11eb-8357-15ae77a2207b.png)
# web3j-maven-plugin
[![Build Status](https://travis-ci.org/web3j/web3j-maven-plugin.svg?branch=master)](https://travis-ci.org/web3j/web3j-maven-plugin)
[![codecov.io](https://codecov.io/github/web3j/web3j-maven-plugin/coverage.svg?branch=master)](https://codecov.io/github/web3j/web3j-maven-plugin?branch=master)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

web3j maven plugin is used to create java classes based on the solidity contract files.

## Usage
The base configuration for the plugin will take the solidity files from `src/main/resources` and generates 
the java classes into the folder `src/main/java`.

## Getting Started

Create a standard java maven project. Add following `<plugin>` - configuration into the `pom.xml` file:
#web3j Maven plugin 的pom.xml檔案，執行此檔才能在Java中使用Web3j的套件

```xml
<plugin>
    <groupId>org.web3j</groupId>
    <artifactId>web3j-maven-plugin</artifactId>
    <version>4.8.1</version>
    <configuration>
        <packageName>com.zuehlke.blockchain.model</packageName>
        <sourceDestination>src/main/java/generated</sourceDestination>
        <nativeJavaType>true</nativeJavaType>
        <outputFormat>java,bin</outputFormat>
        <soliditySourceFiles>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.sol</include>
            </includes>
        </soliditySourceFiles>
        <abiSourceFiles>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.json</include>
            </includes>
        </abiSourceFiles>
        <outputDirectory>
            <java>src/java/generated</java>
            <bin>src/bin/generated</bin>
            <abi>src/abi/generated</abi>
        </outputDirectory>
        <contract>
            <includes>
                <include>greeter</include>
            </includes>
            <excludes>
                <exclude>mortal</exclude>
            </excludes>
        </contract>
        <pathPrefixes>
            <pathPrefix>dep=../dependencies</pathPrefix>
        </pathPrefixes>
    </configuration>
</plugin>
```
Web3j 原始碼的生成指令

![1_IVmYRWgQ4yw_aaUNJXdMfw](https://user-images.githubusercontent.com/82329310/122502299-f1dd1800-d028-11eb-9fe1-72233e3e3910.png)

系統操作流程

![2021-06-27 (9)](https://user-images.githubusercontent.com/82329310/123538168-12624c00-d766-11eb-8a3d-95fed0ada35a.png)

執行程式後會看到登入畫面，在文字框內輸入自己帳號的私鑰便可登入。

![2021-06-16 (12)](https://user-images.githubusercontent.com/82329310/122497022-5004fd80-d01f-11eb-812d-2b501348c725.png)

如果登入者微系統預設管理者的私鑰則會出現部屬合約的視窗，管理者輸入候選人的名字後發布合約(預設候選人數為三個)。

![2021-06-18 (2)](https://user-images.githubusercontent.com/82329310/122495379-81c89500-d01c-11eb-969b-37ab40ff9373.png)

看到跳出視窗代表合約部屬成功

![2021-06-27 (3)](https://user-images.githubusercontent.com/82329310/123538182-28700c80-d766-11eb-9ec9-1bd1f72aa62e.png)
![2021-06-27 (5)](https://user-images.githubusercontent.com/82329310/123538192-31f97480-d766-11eb-8aaa-2d46800b755e.png)

接著管理者可以看到管理者的操縱畫面，有start ballot 跟 end ballot兩個按鈕，管理者按下 start ballot 後投票者才能開始投票，當管理者按下結束投票，管理者視窗會跳出最終結果畫面。
但如果投票人要看到投票結果要按下顯示選舉結果按鈕，如果投票已經結束，才會顯示出結果視窗。另外refresh按鈕可以讓管理者在部屬合約時更新管理者畫面。

![2021-06-27 (8)](https://user-images.githubusercontent.com/82329310/123538199-3cb40980-d766-11eb-877e-61b04d12cabd.png)

結果頁面有每個候選人獲取的票數和當選者的名字顯示在最上方。

#程式無法運行在開發時使用的測試鏈以外的區塊練網路，如果要切換區塊鏈網路，必須更改程式中預設的管理者私鑰。

#由於沒有IP進行訊息傳輸，且localhost已被測試鏈佔據，合約部屬後的地址無法同步寫入程式中，部屬後要進入程式碼中更改合約地址(字串CONTRACT_ADDRESS)。




