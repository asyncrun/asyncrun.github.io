---
layout: post
title: Unity后台运行
categories: [Unity]
description: Unity后台运行、失焦点和Timer的一些测试
keywords: Unity
---
这段代码主要验证几个问题：
1、`Application.runInBackground`在Editor模式下切换后台是否运行
2、`Time.realtimeSinceStartup`与`Time.time`的区别
3、`Time.timeScale`变化对`Time.realtimeSinceStartup`与`Time.time`的影响

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;
    
    public class test : MonoBehaviour
    {
        public void Awake()
        {
            Application.runInBackground = true;
        }
    
        private float delteTime = 0;
        private float lastTimerealtimeSinceStartup  = 0;
        private float eTime = 0;
        private string text = "-";
    
        public void Update()
        {
            delteTime = Time.realtimeSinceStartup - lastTimerealtimeSinceStartup;
            lastTimerealtimeSinceStartup = Time.realtimeSinceStartup;
    
            eTime += delteTime;
    
            //每秒打印一次
            if (eTime >= 1f)
            {
                text = "Time.realtimeSinceStartup : " + Time.realtimeSinceStartup
                                                      + " | Time.time : " + Time.time;
    
                Debug.Log(text);
    
                eTime -= 1f;
            }
        }
    	public void OnGUI()
        {
            if (GUILayout.Button("set time scale 3"))
            {
                Time.timeScale = 3;
            }
            
            if (GUILayout.Button("set time scale 2"))
            {
                Time.timeScale = 2;
            }
    
            if (GUILayout.Button("set time scale 1"))
            {
                Time.timeScale = 1;
            }
    
            if (GUILayout.Button("set time scale 0.5f"))
            {
                Time.timeScale = 0.5f;
            }
    
            if (GUILayout.Button("set time scale 0."))
            {
                Time.timeScale = 0.0f;
            }
            
            if (GUILayout.Button("Application.runInBackground = true"))
            {
                Application.runInBackground = true;
            }
    
            if (GUILayout.Button("Application.runInBackground = false"))
            {
                Application.runInBackground = false;
            }
    
            GUILayout.TextField(text);
        }
    }


---
结论
1、`Application.runInBackground`在Editor中true时后台运行，false时后台不运行，切后台就是失去焦点
2、`Time.realtimeSinceStartup`与`Time.time`在`Time.timeScale = 1`时，时间是不一样的
3、`Time.timeScale`变化对`Time.realtimeSinceStartup`没影响
4、`Time.timeScale`变化对`Time.time`有影响
5、切到后台Time.time不再变化
6、`Application.runInBackground`在Android与iOS不起作用


