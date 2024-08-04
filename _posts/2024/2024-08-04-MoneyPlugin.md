---
layout: post
title:	"Minecraft Plugin Money System"
date:	2024-08-04 09:29:24
categories:
    - blog
tags:
    - learning
    - knowledge
    - game
---
# 현재 코드
Money.java
```java
package law.com.mcplugin0721;
import java.io.*;
import java.util.Arrays;
import java.util.UUID;

public class Money {
    UUID uuid;
    int money;

    public static void checkPlayer() {

    }

    public static void makeAndWriteFile(UUID[] uuid, int[] money) {
        String path = System.getProperty("user.dir");
        File file = new File(path);
        try {
            if (file.createNewFile()) {
                System.out.println("File created. Try to write in");
                BufferedWriter BW = new BufferedWriter(new FileWriter(file));
                StringBuilder TEXT = new StringBuilder();
                for(int i=0;i<money.length;i++) {
                    TEXT.append(uuid[i]).append('\n');
                    TEXT.append(money[i]).append('\n');
                }
                BW.write(String.valueOf(TEXT), 0, TEXT.length());
            } else {
                System.out.println("File already exists. Try to edit.");
                BufferedWriter BW = new BufferedWriter(new FileWriter(file));
                StringBuilder TEXT = new StringBuilder();
                for(int i=0;i<money.length;i++) {
                    TEXT.append(uuid[i]).append('\n');
                    TEXT.append(money[i]).append('\n');
                }
                BW.write(String.valueOf(TEXT), 0, TEXT.length());
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static UUID[] readFileUUID(File file) throws IOException {
        UUID[] uuids = new UUID[100];
        BufferedReader BR = new BufferedReader(new FileReader(file));
        String str = String.valueOf(BR.read()); int i=0; int j=0;
        String[] Words = new String[200];
        while(str.charAt(i) != '\0') {
            while(str.charAt(i) != '\n') {
                Words[j] += str.charAt(i);
                i++;
            }
            j++;
        } j=0;
        for(int k=0;k<i+1;k++) {
            if(k % 2 != 0) {
                uuids[j] = UUID.fromString(Words[k]);
                j++;
            }
        }
        return uuids;
    }
    public static int[] readFileMoney(File file) throws IOException {
        int[] money = new int[100];
        BufferedReader BR = new BufferedReader(new FileReader(file));
        String str = String.valueOf(BR.read()); int i=0; int j=0;
        String[] Words = new String[200];
        while(str.charAt(i) != '\0') {
            while(str.charAt(i) != '\n') {
                Words[j] += str.charAt(i);
                i++;
            }
            j++;
        } j=0;
        for(int k=0;k<i+1;k++) {
            if(k % 2 != 0) {
                money[j] = Integer.parseInt(Words[k]);
                j++;
            }
        }
        return money;
    }
}
```