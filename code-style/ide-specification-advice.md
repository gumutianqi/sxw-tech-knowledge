# IDE 规范建议

> Author: larry.koo  Date: 2017-11-08

---

### 源代码文件规范

> 统一使用以下生学教育科技有限公司的文件头规范

```
/*
 * 四川生学教育科技有限公司
 * Copyright (c) 2015-2025 Founder Ltd. All Rights Reserved.
 *
 * This software is the confidential and proprietary information of
 * Founder. You shall not disclose such Confidential Information
 * and shall use it only in accordance with the terms of the agreements
 * you entered into with Founder.
 *
 */
```

**配置方式**

打开 `IDEA`，通过File 》 Import Settings 导入配置好的文件模版文件 file-template-setting.jar 文件，重启即可；

[文件模版文件点击下载](/assets/file-template-settings.jar)

### 注释规范

**文件注释**

> 文件注释必须包含 描述（@description）、时间（@date）、作者（@author）、起始版本(@since), 示例如下：

```
/**
 * @description TODO
 * @date 2017/11/8 17:51
 * @slogon 站在巨人的肩膀上
 * @author LarryKoo (larrykoo@126.com)
 * @since 1.0.x
 */

```

**其他注释需要遵循 JavaDoc 规范**

### JAVA Package 规范

约定每个 Java package 下面必须包含一个`package-info.java` 文件来标识该 package 的所包含的内容；提交的代码不得出现空的 package 目录；







