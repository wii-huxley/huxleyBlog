title: 友盟微社区 v2.6 论坛版接入笔记
categories: android
tags:
  - android
  - umeng
---

## 准备工作 ##

进入 [友盟微社区官网][] 获取 `Appkey` 和 [友盟微社区Android SDK][]， `Android Studio` 版集成：解压文件 `umeng_community_android_social_sdk_2.6_arm64_custom` 。import module `umeng_community_library_project` ，删除无关的 jar 包（只需留下`httpmime`,`umeng_activeandroid`,`umeng_community_sdk_core`,`umeng_community_sdk_db`,`universal_image_loader`），将 `opensource` 下的 `umeng_community_android_ui_discuss`和 `umeng_community_android_ui_main` 相关文件复制到module中，便可开始深度定制。

---

## 开始深度定制 ##

### 各个页面的文件 ###

*	`我的` ： 
	*	activity：FindActivity
	*	layout：umeng_comm_find_layout
	*	titleString：umeng_comm_mine
*	`主页`：
	*	activity：CommunityMainFragment
	*	layout：umeng_comm_community_frag_layout
	*	titleLayout：umeng_comm_fragment_title


[友盟微社区官网]: https://wsq.umeng.com/communities/pro/home/
[友盟微社区Android SDK]: http://dev.umeng.com/wsq/android/sdk-download