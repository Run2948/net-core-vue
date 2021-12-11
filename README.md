## **1.创建前端项目**

打开VS2022， 在新建项目窗口搜索"Standalone"，可以看到React/Angular/Vue.js的项目模板，并可选择使用JS还是TS：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPUIoYyicJQnNqRoofTL3R8SD0DWJjGLccqRzWlJY2ajG7ZDd2t6g7Skw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

*下面还是以Vue.js为例讲解，其他前端框架同样操作。*

选择“Standalone TypeScript Vue Template”，在“其他信息”窗口，一定要记住勾选**Add integration for Empty ASP.NET Web API Project**: 

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPNtjuecMcEAcpAU9NorUdIibxGfD41mJDaaUqsflUOAg0t2dAmN8rPSQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

点击“创建”按钮后，会自动执行vue CLI下载相关依赖： 

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPAGoywDvL5rq3yz02op2hDZ6dISzWCTuia7zlMFodlBcFNFT07ibialtibQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**创建完成后，你会发现只有前端项目。****后端在哪？**

## **2.添加后端项目**

在解决方案资源管理器，右键点击解决方案名称，选择"添加"->"新建项目"，选择“ASP.NET Core Web API”，按照正常方式创建Web API项目。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPsz0ZsJVY29K3m0ogVw67ubgKPcxIQYIJjfPGIQjXb14rahI3jfSOoA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

OK，前后端项目已经创建完成了，项目结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPTNPdv1UmSGqvy01niajDzMtd5kucSRJBafqxyBibG4B3S4ubfjHLUAKg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**但是，想要能够实现集成调试，我们还需要进行如下操作。**

## **3.调试**

打开WebApplication1项目Properties目录下的`launchSettings.json`文件，找到API启动地址：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPYVcrH7vPkkK1PkCcc0IAzTjBloeouXtetMwNGDwEZ0QTeCicwXxaYKg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

然后，打开vueproject1项目的vue.config.js，修改proxy为对应地址：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPFCjGFZ2Pe8vV6s3kvgtGJibLw4C7icxjfOET6SYdW70PJs6cv5J2C2JQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

接着，右键点击解决方案名称，选择"属性"，修改为多个启动项目：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPxsPm6GKU9NjFibsoTBPtb2G16kfFevHbMic2Vt9QHxqHbzSMrlfIrE2A/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后，F5启动解决方案，可以看到访问了正确的后端服务：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPVISicOscx1iaoVhvib8zYMAZfgZRPvYEgk5M1Hf5STtCDqH8kGa9nacZw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**但是，别高兴太早，虽然调试成功了，要想部署成前后端集成项目，我们还要做点工作。**

## **4.部署**

打开vueproject1项目的vue.config.js，修改module.exports，增加outputDir，值为"../WebApplication1/wwwroot"：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPjjFa4K6Xrt9d5vBtibiaY0RfdUZPST2IfjjSVVLGkrudNv66H5nDoz2w/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**它的作用，是将前端部署文件输出到Web API指定目录。**

然后，修改WebApplication1项目的Program.cs，加入如下代码：

```
app.UseDefaultFiles();
app.UseStaticFiles();
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHP3iaedVmR4iaT8b6blP0WT3xLjt92ibzBcPe9xSpDf2uClQziaDO4QcoMxw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**它的作用，是启用静态文件服务，由Web API承载前端文件显示。**

最后，修改WebApplication1.csproj文件，增加如下内容：

```
<Target Name="PublishRunWebpack" AfterTargets="ComputeFilesToPublish">
    <Exec WorkingDirectory="$(ProjectDir)\..\vueproject1" Command="npm run build -- --prod" />

    <ItemGroup>
        <DistFiles Include="wwwroot\**" />
        <ResolvedFileToPublish Include="@(DistFiles->'%(FullPath)')" Exclude="@(ResolvedFileToPublish)">
            <RelativePath>%(DistFiles.Identity)</RelativePath>
            <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
        </ResolvedFileToPublish>
    </ItemGroup>
</Target>
```

**它的作用，是发布Web API时自动编译前端项目，并将wwwroot所有文件复制到发布目录下。**

**现在，就是见证奇迹的时刻。**

执行WebApplication1的发布操作，它会自动执行`npm run build`，将前端代码编译输出到`wwwroot`目录下，发布目录结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHP1LibePpXlUO5DekialUdpo4D7x53TNyZrVwnIJ7AGPvy8z8iakTm3ru0A/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

运行WebApplication1.exe，访问http://localhost:5000，可以看到调用的还是相同端口下的后端API：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/lB5L72GibpKhhibHpJKODNDJsGjR8HFlHPMTz31MicMVP9apk717M1RVKNCUHrhmZkINnkgWdKmsC28JuTQPsdMgw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# 结论

虽然VS2022没有提供前后端集成项目模板，但是，经过我们的改造，同样可以轻松实现React/Angular/Vue.js + Web API前后端集成。

