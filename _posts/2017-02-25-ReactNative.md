---
layout: post
title: ��װReact-Native
date: 2017-2-25
categories: blog
tags: [��¼]
---

��Ҫ�ο�[React-Native�ٷ������ĵ�](https://reactnative.cn/docs/0.41/getting-started.html#content)��
# ��һ�� ����Nodejs��npm
[Nodejs���ص�ַ](https://nodejs.org/download/release/v7.6.0/)
[npm���ص�ַ](https://nodejs.org/dist/npm/)
ѡ���ʺ��Լ��汾�����أ�ò�����µ�Nodejs���Ѿ�����npm���������npm��װģ���ʱ����ִ���������ΪNodejs�汾����ע��x64�ĵ�������64-bit�ģ�x86�ĵ�������32-bit�ġ�(https://nodejs.org/en/download/)
����Ƿֿ����صģ���npm�ļ��зŵ�C:\Program Files (x86)\nodejs\node_modules��
#�ڶ��� ���ذ�װJDK
����CMD������java -version���Բ鿴��û�а�װ��JDK�����û�еĻ���ȥ[����](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)����һ��1.8�汾�ġ�Ȼ��·����ӵ�����������
#������ ����Android SDK�Ͱ�װAndroid Studio
[Andriod Studio���ص�ַ](https://developer.android.com/studio/index.html#downloads)
������ص�Android Studioû���Դ�SDK����ô���ص�ַ���������Ǵ�SDK��
��װAndroid Studio��ʱ��ע�ⲻҪ��·���д������ģ����ǳ���Ҫ��
#���Ĳ�  ���չ����̲�����Android Studio
��
#���岽 ��װReact-Native
CMD������(����ڹ���Ա��ݴ�)npm install -g react-native-cli������˵npm���Ǹ��ö�������
#������ ��������
���ȴ�Android Studioģ������һ��Ҫ�ȿ���ģ������������
Ȼ��ѡ��һ��Ŀ¼������
<code>
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
</code>
�����ʱ���ܹ��������У��Ǿ�л��л���ˡ�˵����Ʒ�ܺá��ҵ�ʱ������һ��������
```
ENOENT: no such file or directory, open react-native 'C:\TDM-GCC-64\BIN;C:MINGW\BIN;C:User\AppData\Local\Temp'
```
��������ɶ���������ȥStackOverflow��Ҳû�ҵ��𰸡����ǿ����ò�ƺ���Ϥ��·�����򿪻������������ֹ�Ȼ��������TEMP������·����ɾ�����·��������react-native run-android. nice! ��������!

#�Ľ�
���ݹ�������ʾ���ظ�[genymotion](https://www.genymotion.com/download/)���򿪺�Addһ�����ʵİ汾����������Android StudioҲ���ÿ��ˡ� nice!

#�ܽ�
������Ҫ���������Щ������û�������˾�����ţ���ȻŪ��һ���춼�겻�ɣ���������Ҳ��֪������ô�졣���֮�£�react.js�İ�װҪ���׵ö��ˡ�