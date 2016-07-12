---
layout: post
title:  "Spring学习笔记---文件上传"
date:   2016-07-11 22:00:00
categories: JavaWeb
tags: Spring
author: 薛彬
---

* content
{:toc}

说是Spring的学习笔记，其实就没涉及到多少Spring的知识。。实现了一个将zip包上传到服务器上并解压的功能。。





我们先在html中写一个表单，通过表单的形式来上传：

```html
<form action="/upload.do?"enctype="multipart/form-data" method="post">
    <p>
        选择文件：<input type="file" name="filename">
    </p>
    <input type="submit" value="上传">
</form>
```

然后就可以开始写后台程序了,为了不繁琐只贴出有用的代码：

```java
//  url:/upload.do?filename=??
@RequestMapping(value="/upload.do",method=RequestMethod.POST)
    public void upload(@RequestParam("filename") MultipartFile upload_file,HttpServletResponse response){
    if(!upload_file.isEmpty()){
        String uuid = UUID.randomUUID().toString();
		String tmpDir = System.getProperty("java.io.tmpdir") + File.separator + uuid;
        String recv_filename=upload_file.getOriginalFilename();
        String firstDir;
        try{
            String filepath=tmpDir+File.separator;
            if(!new File(filepath).exists()){
                new File(filepath).mkdir();
            }
            String path=filepath+recv_filename;
            upload_file.transferTo(new File(path));
            firstDir=ZipUtils.unzip(path,tmpDir);
            if(null == firstDir || firstDir.isEmpty()){
            }else{
                File srcDir = new File(tmpDir + File.separator + firstDir);
				File destDir = new File();
				destDir.mkdirs();
				FileUtils.copyDirectory(srcDir, destDir);
				FileUtils.forceDelete(srcDir);
            } 
        }catch(IllegalStateException | IOException e1){
        }finally{
            try{
                FileUtils.forceDelete(new File(tmmDir));
            }catch(IOException e){}
        }
    }
}
```