---
title: "Java建立URL请求"
date: 2017-10-29
categories: Documentation
tags:
- lab
---



# 简述：

## 使用Java写 向后台服务做GET和POST请求

# 代码：
## Test1.java
## 建立Http Connection， 向后台的Servlet做出Get请求

package test.java_request;

import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.logging.Level;
import java.util.logging.Logger;

class StreamToString{
    public static String ConvertToString(InputStream inputStream){
        InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
        BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
        StringBuilder result = new StringBuilder();
        String line = null;
        try {
            while((line = bufferedReader.readLine()) != null){
                result.append(line + "\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try{
                inputStreamReader.close();
                inputStream.close();
                bufferedReader.close();
            }catch(IOException e){
                e.printStackTrace();
            }
        }
        return result.toString();
    }


    public static String ConvertToString(FileInputStream inputStream){
        InputStreamReader inputStreamReader = new InputStreamReader(inputStream);
        BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
        StringBuilder result = new StringBuilder();
        String line = null;
        try {
            while((line = bufferedReader.readLine()) != null){
                result.append(line + "\n");
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try{
                inputStreamReader.close();
                inputStream.close();
                bufferedReader.close();
            }catch(IOException e){
                e.printStackTrace();
            }
        }
        return result.toString();
    }
}

public class Test1 {
    public static void main(String[] args) {
        try{
            URL url = new URL("http://localhost:8090/MyWebProject/Test");
            HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
            //GET Request Define:
            urlConnection.setRequestMethod("GET");
            urlConnection.connect();

            //Connection Response From Test Servlet
            System.out.println("Connection Response From Test Servlet");
            InputStream inputStream = urlConnection.getInputStream();

            //Convert Stream to String
            String responseStr = StreamToString.ConvertToString(inputStream);
            System.out.println(responseStr);
        }catch(IOException e){
            Logger.getLogger(Test1.class.getName()).log(Level.SEVERE, null, e);
        }
    }
}