---
layout: post
title:	"ImplementLOLwithJava"
date:	2024-06-23 10:02:24
categories:
    - blog
tags:
    - learning
    - java
---
# 1번 문제
## 지문: 
페이커는 랭크 게임을 하기위해 롤에 접속했습니다.
랭크게임을 하기위해 게임을 시작했는데요.(픽창으로 넘어감)

픽창으로 넘어간뒤 페이커의 포지션을 랜덤으로 출력하시오.
(문제가 이해가 되지않으면 출력과 예를 확인하고 코딩하시오.)

콘솔창 예)
```text
ex1
게임을 시작 하시겠습니까? 1)예, 2)아니오

예, 매칭을 시작하겠습니다.

게임이 매칭되었습니다.
페이커님의 포지션은 탑 입니다.

ex2
게임을 시작 하시겠습니까? 1)예, 2)아니오

예, 게임을 매칭중입니다…………….

게임이 매칭되었습니다.
페이커님의 포지션은 서포터 입니다.
```

## 풀이 코드:
```java
import java.util.Scanner;
import java.util.Random;

public class Main {
    public static void main(String[] args) { // 최초 실행점
        String Position[] = {"탑","정글","미드","원거리딜러","서포터"};
        Random random = new Random();
        random.setSeed(System.currentTimeMillis());
        Scanner sc = new Scanner(System.in);
        System.out.print("게임을 시작 하시겠습니까? 1)예, 2)아니오 -> ");
        int A = sc.nextInt();
        if(A == 1) {
            System.out.println("예, 매칭을 시작하겠습니다.");
        } else if(A == 2) {
            System.out.print("게임을 종료합니다.");
            System.exit(1);
        } else {
            System.out.print("올바른 값이 아닙니다.");
            System.exit(1);
        }
        System.out.println("게임이 매칭되었습니다.");
        int pos = random.nextInt(5);
        System.out.printf("페이커님의 포지션은 %s 입니다",Position[pos]);

    }
}
```

# 2번 문제
## 지문: 
조건을 하나 추가해보겠습니다.
(롤에는 일반게임, 랭크, 우르프, 단일챔피언, AI 모드가 있다.)
페이커는 게임을 하기위해 접속했다.
페이커가 선택한 게임과 지정된 포지션, 지정된 팀을 랜덤으로 나타내시오.
(문제가 이해가 되지않으면 출력과 예를 확인하고 코딩하시오.)

콘솔창 예)
```text
게임을 선택해 주세요.
1.일반게임
2.랭크게임
3.우르프
4.단일챔피언
5.AI

일반게임을 선택했습니다. 일반게임을 매칭을 하겠습니다………………….

게임이 매칭되었습니다.
페이커님의 포지션은 미드이고 블루팀입니다.
```

## 풀이 코드:
```java
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) { // 최초 실행점
        String Position[] = {"탑","정글","미드","원거리딜러","서포터"};
        String Teams[] = {"블루","레드"};
        String Games[] = {"일반게임","랭크게임","우르프","단일챔피언","AI"};
        Random random = new Random();
        random.setSeed(System.currentTimeMillis());
        Scanner sc = new Scanner(System.in);
        System.out.print("게임을 선택해주세요. ");
        for(int i=0;i<5;i++) {
            System.out.printf("%d.%s ",i+1,Games[i]);
        } System.out.print(" -> ");
        int A = sc.nextInt();
        if(A < 6) {
            System.out.printf("%s을/를 선택했습니다. %s을/를 매칭을 하겠습니다.\n", Games[A], Games[A]);
        } else {
            System.out.print("올바른 값이 아닙니다.");
            System.exit(1);
        }
        System.out.println("게임이 매칭되었습니다.");
        int pos = random.nextInt(5); int team = random.nextInt(2);
        System.out.printf("페이커님의 포지션은 %s이고 %s팀입니다",Position[pos],Teams[team]);

    }
}
```

# 3번 문제
## 지문: 
페이커는 혼자 게임을 하는것이 재미가 없어서 친구들에게 카톡으로 연락했습니다.
페이커는 X명의 파티원을 구했습니다.

이제 페이커는 파티원들과 게임을 시작하는데요.
문제 1번 2번의 조건을 합쳐 팀의 위치, 파티원들의 포지션을 랜덤으로 나타내시오

*파티는 총 페이커를 포함 5명까지 가능하다.
*파티 구성 인원이 4명 이하일 경우 외부인원의 포지션도 정해져야 한다.

콘솔창 예)
```text
파티원의 수를 정해주세요 : 3

게임을 선택해주세요.
1.일반게임
2.랭크게임
3.우르프
4.단일챔피언
5.AI

랭크게임을 선택했습니다. 랭크게임을 매칭을 하겠습니다………………….

게임이 매칭되었습니다.

팀 진영은  블루팀입니다.

페이커님의 포지션은 미드
파티원1의 포지션은 정글
파티원2의 포지션은 탑
외부인1의 포지션은 원딜
외부인2의 포지션은 서포터
```
*파티원 수가 3명이기 때문에 외부인이 2명 추가됬다.
*파티원 수가 5명이면 외부인은 0이다.

## 풀이 코드: 
```java
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) { // 최초 실행점
        game: while(true) {
            int Party = 0;
            String Position[] = {"탑","정글","미드","원거리딜러","서포터"};
            String Teams[] = {"블루","레드"};
            String Games[] = {"일반게임","랭크게임","우르프","단일챔피언","AI"};
            Random random = new Random();
            random.setSeed(System.currentTimeMillis());
            Scanner sc = new Scanner(System.in);
            System.out.print("파티원의 수를 정해주세요 : ");
            Party = sc.nextInt();
            String[] Names = new String[5];
            Names[0] = "페이커";
            for(int i=1;i<5;i++) {
                if(Party > i) {
                    Names[i] = "파티원"+i;
                } else {
                    Names[i] = "외부인"+i;
                }
            }
            System.out.print("게임을 선택해주세요. ");
            for(int i=0;i<5;i++) {
                System.out.printf("%d.%s ",i+1,Games[i]);
            } System.out.print(" -> ");
            int A = sc.nextInt();
            if(A < 6) {
                System.out.printf("%s을/를 선택했습니다. %s을/를 매칭을 하겠습니다.\n", Games[A], Games[A]);
            } else {
                System.out.print("올바른 값이 아닙니다.");
                System.exit(1);
            }
            System.out.println("게임이 매칭되었습니다.\n");
            int[] posSet = new int[5]; int team = random.nextInt(2);
            System.out.printf("팀 진영은 %s팀입니다\n\n",Teams[team]);
            for(int i=0;i<5;i++) {
                posSet[i] = random.nextInt(5);
                for(int j=0;j<i;j++) {
                    if(posSet[i] == posSet[j]) {
                        i--; break;
                    }
                }
            }
            for(int i=0;i<5;i++) {
                System.out.printf("%s님의 포지션은 %s\n", Names[i], Position[posSet[i]]);
            }
            break game;
        }
    }
}
```

# 4번 문제
## 지문: 
롤을 하면서 한번에 게임이 매칭이 되는 경우가 있지만, 다시 매칭을 해야하는 경우가 있다.
문제 1,2,3 번의 조건을 만족하고 랜덤으로 매칭이 취소되고 4초뒤에 다시 매칭을 시작한다.

콘솔창 예)
```text
파티원의 수를 정해주세요 : 3

게임을 선택해주세요.
1.일반게임
2.랭크게임
3.우르프
4.단일챔피언
5.AI

랭크게임을 선택했습니다. 랭크게임을 매칭을 하겠습니다………………….

......누군가 게임을 취소해 다시 매칭을 시작합니다.…..

게임이 매칭되었습니다.

팀 진영은  블루팀입니다.

페이커님의 포지션은 미드
파티원1의 포지션은 정글
파티원2의 포지션은 탑
외부인1의 포지션은 원딜
외부인2의 포지션은 서포터
```
*파티원 수가 3명이기 때문에 외부인이 2명 추가됬다.
*파티원 수가 5명이면 외부인은 0이다.

## 풀이 코드:
```java
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) { // 최초 실행점
        game: while(true) {
            int Party = 0;
            String Position[] = {"탑","정글","미드","원거리딜러","서포터"};
            String Teams[] = {"블루","레드"};
            String Games[] = {"일반게임","랭크게임","우르프","단일챔피언","AI"};
            Random random = new Random();
            random.setSeed(System.currentTimeMillis());
            Scanner sc = new Scanner(System.in);
            System.out.print("파티원의 수를 정해주세요 : ");
            Party = sc.nextInt();
            String[] Names = new String[5];
            Names[0] = "페이커";
            for(int i=1;i<5;i++) {
                if(Party > i) {
                    Names[i] = "파티원"+i;
                } else {
                    Names[i] = "외부인"+i;
                }
            }
            System.out.print("게임을 선택해주세요. ");
            for(int i=0;i<5;i++) {
                System.out.printf("%d.%s ",i+1,Games[i]);
            } System.out.print(" -> ");
            int A = sc.nextInt();
            if(A < 6) {
                System.out.printf("%s을/를 선택했습니다. %s을/를 매칭을 하겠습니다.\n", Games[A], Games[A]);
            } else {
                System.out.print("올바른 값이 아닙니다.");
                System.exit(1);
            }

            try {
                int cancel = random.nextInt(5);
                boolean party_canceled;
                if(cancel < Party) {
                    party_canceled = true;
                } else {
                    party_canceled = false;
                }
                if(cancel != 0) {
                    if(party_canceled) {
                        System.out.println("......우리 파티원이 게임을 취소했습니다.…..");
                        continue game;
                    } else {
                        System.out.println("......누군가 게임을 취소해 다시 매칭을 시작합니다.…..");
                        Thread.sleep(4000); // 4초
                    }
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("게임이 매칭되었습니다.\n");
            int[] posSet = new int[5]; int team = random.nextInt(2);
            System.out.printf("팀 진영은 %s팀입니다\n\n",Teams[team]);
            for(int i=0;i<5;i++) {
                posSet[i] = random.nextInt(5);
                for(int j=0;j<i;j++) {
                    if(posSet[i] == posSet[j]) {
                        i--; break;
                    }
                }
            }
            for(int i=0;i<5;i++) {
                System.out.printf("%s님의 포지션은 %s\n", Names[i], Position[posSet[i]]);
            }
            break game;
        }
    }
}
```

# 5번 문제
## 지문:
소환사의협곡에 오신것을 환영합니다.

페이커의 포지션은 미드이고 야쓰오를 선택했습니다.
페이커의 기본공격은 100입니다.
상대 캐릭터 탈론의 체력은 1000입니다.

페이커의 야쓰오는 상대캐릭터 탈론을 몇 대를 때려야 잡을수 있을까요?

1. 아이템을 구매한다.
2. 숫자1을 입력받아 공격한다.

아이템 리스트

아이템	공격력	가격
도란링	  +1	  400
도란검	  +5	  400
도란방패	-10	  450
신발	    +0   300

콘솔창 예)
```text
페이커의 포지션은 미드이고 야쓰오를 선택했습니다.
페이커의 기본공격은 100입니다.
상대 캐릭터 탈론의 체력은 1000입니다.

도란검을 선택했습니다.

1
공격을 시작합니다. 적에게 준 피해량 105, 탈론의 남은체력 895.

1
공격을 시작합니다. 적에게 준 피해량 105, 탈론의 남은체력 790.

……………..

1
공격을 시작합니다. 적에게 준 피해량 105, 탈론의 남은체력 160.

1
공격을 시작합니다. 적에게 준 피해량 105, 탈론의 남은체력 55.

1
공격을 시작합니다. 적에게 준 피해량 105, 탈론의 남은체력 0. 탈론이 죽었습니다.

승리
```


## 풀이 코드:
### Champion.java
```java
public class Champion {
    int health;
    int damage;
}
```


### Main.java
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        System.out.println("페이커의 포지션은 미드이고 야쓰오를 선택했습니다");
        System.out.println("페이커의 기본공격은 100입니다.");
        System.out.println("상대 캐릭터 탈론의 체력은 1000입니다.");
        Champion yasuo = new Champion();
        Champion talon = new Champion();
        yasuo.damage = 100; yasuo.health = 1;
        talon.health = 1000; talon.damage = 1;
        Scanner sc = new Scanner(System.in);
        int Item_Input = sc.nextInt();
        if(Item_Input > 5 || Item_Input < 1) {
            System.out.println("올바른 아이템 값이 아닙니다.");
            System.exit(1);
        }
        switch (Item_Input) {
            case 1:
                System.out.println("도란링을 선택했습니다.");
                yasuo.damage += 1;
                break;
            case 2:
                System.out.println("도란검을 선택했습니다.");
                yasuo.damage += 5;
                break;
            case 3:
                System.out.println("도란방패를 선택했습니다.");
                yasuo.damage -= 10;
                break;
            case 4:
                System.out.println("신발을 선택했습니다.");
                break;
        }
        while(talon.health != 0) {
            int a = sc.nextInt();
            if (a == 1) {
                talon.health -= yasuo.damage;
                if(talon.health < 0) talon.health = 0;
                System.out.printf("공격을 시작합니다. 적에게 준 피해량 " + yasuo.damage + ", 탈론의 남은체력 " + talon.health + ".");
                if(talon.health != 0) {
                    System.out.println("\n");
                } else {
                    System.out.println(" 탈론이 죽었습니다.");
                }
            }
        }
        System.out.print("\n승리");


    }
}
```

# 6번 문제
## 지문:
소환사의협곡에 오신것을 환영합니다.

페이커의 포지션은 미드이고 제드를 선택했습니다.
상대 캐릭터는 코르키입니다.

라인전의 결과를 출력하시오.

조건 1
대결 시작을 하면 2초마다 제드와 코르키가 서로 공격한다. 서로에게 피해를 입히고 먼저 체력이 0이되는 캐릭터가 라인전에서 패배

공격력 공식 = 캐릭터 스펙의 공격력 - 난수발생숫자

조건 2
코르키가 먼저 때린다.

캐릭터 스펙
캐릭터	공격력	체력
코르키	120	1000
제드	150	700

   난수발생) 1. int a=(int)(Math.random()*100) : 0 - 99 사이의 난수
                   2. ① import java.util.Random;
                      ② Random 변수1 = new Random();
                      ③ int 변수2 = 변수1.nextInt(최대값); 
                               ==>  0 ~ (최대값 - 1)사이의 임의의 수


콘솔창 예)
```text
대결을 시작합니까? 1:시작, 2:탈주

(2초뒤)
미니언이 생성되었습니다.

코르키 -> 제드 20의 피해 (코르키체력 : 1000, 제드체력 : 680)
제드 -> 코르키 30의 피해(코르키체력 : 970, 제드체력 : 680)

…………………..



제드 -> 코르키 10의 피해(코르키체력 : 80, 제드체력 : 0)
코르키 라인전 승리
```

## 풀이 코드: 
### Champion.java
```java
public class Champion {
    int damage;
    int health;
}
```

### Main.java
```java
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws InterruptedException { // 최초 실행점
        System.out.print("라인전을 시작합니까? 1) 시작, 2) 탈주 -> ");
        Scanner sc = new Scanner(System.in);
        int MatchStart = sc.nextInt();
        if(MatchStart == 2) {
            System.out.println("탈주하였습니다.");
            System.exit(0);
        } else if(MatchStart != 1) {
            System.out.println("올바른 값이 아닙니다.");
            System.exit(1);
        } else {
            Thread.sleep(2000);
            System.out.println("미니언이 생성되었습니다.\n");
            Champion Zedd = new Champion();
            Champion Corki = new Champion();
            Zedd.damage = 120; Zedd.health = 700;
            Corki.damage = 150; Corki.health = 1000;
            Random random = new Random();
            int turn = 1;
            int random_damage;
            int deal;
            while(Zedd.health != 0 && Corki.health != 0) {
                if(turn % 2 == 1) {
                    random_damage = random.nextInt(100);
                    deal = Corki.damage - random_damage;
                    Zedd.health -= deal;
                    if(Zedd.health < 0) Zedd.health = 0;
                    System.out.printf("코르키 -> 제드 / %d의 피해 (코르키체력: %d, 제드 체력: %d)\n", deal, Corki.health, Zedd.health);

                } else {
                    random_damage = random.nextInt(100);
                    deal = Zedd.damage - random_damage;
                    Corki.health -= deal;
                    if(Corki.health < 0) Corki.health = 0;
                    System.out.printf("제드 -> 코르키 / %d의 피해 (코르키체력: %d, 제드 체력: %d)\n", deal, Corki.health, Zedd.health);
                }
                turn++;
                Thread.sleep(1250);
            }
            if(Zedd.health <= 0) {
                System.out.println("코르키 라인전 승리");
            } else {
                System.out.println("제드 라인전 승리");
            }
        }
    }
}
```

# 7번 문제
## 지문: 
소환사의협곡에 오신것을 환영합니다.

페이커의 포지션은 미드이고 카시오페아를 선택했습니다.
상대 캐릭터는 탈론입니다.

라인전의 결과를 출력하시오.

조건 1
대결 시작을 하면 2초마다 카시오페아와 탈론이 서로 공격한다. 서로에게 피해를 입히고 먼저 체력이 0이되는 캐릭터가 라인전에서 패배

공격력 공식 = 캐릭터 스펙의 공격력 - 난수발생숫자

조건 2
첫번째 난수가 높은 캐릭터가 먼저 때린다.

조건 3
페이커 팀의 정글은 람머스
상대팀의 정글은 마스터이
공격턴 3번에 한번씩 서로 갱을와서 카시오페아와, 탈론의 체력만 깎는다.

캐릭터 스펙
캐릭터	       공격력  	체력
카시오페아	     90	    1000
탈론	          120	    700
람머스	         40     2000
마스터이	      100	     900


콘솔창 예)
```text
대결을 시작합니까? 1:시작, 2:탈주

(2초뒤)
미니언이 생성되었습니다.

탈론 -> 카시오페아 20의 피해 (탈론 : 1000, 카시오페아 : 680)
카시오페아 -> 탈론 30의 피해(탈론 : 970, 카시오페아 : 680)
탈론 -> 카시오페아 20의 피해 (탈론 : 1000, 카시오페아 : 680)
카시오페아 -> 탈론 30의 피해(탈론 : 970, 카시오페아 : 680)
탈론 -> 카시오페아 20의 피해 (탈론 : 1000, 카시오페아 : 680)
카시오페아 -> 탈론 30의 피해(탈론 : 970, 카시오페아 : 680)
람머스 -> 탈론 10의 피해(...)
마스터이 -> 카시오페아 20의 피해 (....)
…………………..



제드 -> 코르키 10의 피해(코르키체력 : 80, 제드체력 : 0)
코르키 라인전 승리
```

## 풀이 코드:
### Champion.java
```java
public class Champion {
    int health;
    int damage;
}

```

### Main.java
```java
import java.util.Scanner;
import java.util.Random;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Random rand = new Random();
        System.out.print("대결을 시작합니까? 1:시작, 2:탈주 ");
        Scanner sc = new Scanner(System.in);
        int GameStart = sc.nextInt();
        if(GameStart == 2) {
            System.out.println("게임을 탈주했습니다.");
            System.exit(0);
        } else if(GameStart != 1) {
            System.out.println("올바른 값이 아닙니다.");
            System.exit(1);
        }
        Champion cassiopeia = new Champion(); cassiopeia.damage = 90; cassiopeia.health = 1000;
        Champion talon = new Champion(); talon.damage = 120; talon.health = 700;
        Champion rammus = new Champion(); rammus.damage = 40; rammus.health = 2000;
        Champion masterYi = new Champion(); masterYi.damage = 100; masterYi.health = 900;
        int turn = 1;
        while(cassiopeia.health != 0 && talon.health != 0) {
            int whoFirst = (int)(Math.random()*1);
            int attack1 = (int)(Math.random()*90); int dmg1 = cassiopeia.damage - attack1;
            int attack2 = (int)(Math.random()*120); int dmg2 = talon.damage - attack2;
            if(whoFirst == 0) {
                talon.health -= dmg1;
                if(talon.health < 0) talon.health = 0;
                System.out.println("카시오페아 -> 탈론 "+dmg1+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                if(talon.health <= 0) break;
                cassiopeia.health -= dmg2;
                if(cassiopeia.health < 0) cassiopeia.health = 0;
                System.out.println("탈론 -> 카시오페아 "+dmg2+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
            } else {
                cassiopeia.health -= dmg2;
                if(cassiopeia.health < 0) cassiopeia.health = 0;
                System.out.println("탈론 -> 카시오페아 "+dmg2+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                if(cassiopeia.health <= 0) break;
                talon.health -= dmg1;
                if(talon.health < 0) talon.health = 0;
                System.out.println("카시오페아 -> 탈론 "+dmg1+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
            }
            if(turn == 3 && (talon.health != 0 && cassiopeia.health != 0)) {
                int attack3 = (int)(Math.random()*40); int dmg3 = rammus.damage - attack3;
                int attack4 = (int)(Math.random()*100); int dmg4 = masterYi.damage - attack4;
                int whoFirst2 = (int)(Math.random()*1);
                if(whoFirst2 == 0) {
                    cassiopeia.health -= dmg4;
                    if(cassiopeia.health < 0) cassiopeia.health = 0;
                    System.out.println("마스터이 -> 카시오페아 "+dmg3+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                    if(cassiopeia.health <= 0) break;
                    talon.health -= dmg3;
                    if(talon.health < 0) talon.health = 0;
                    System.out.println("람머스 -> 탈론 "+dmg4+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                } else {
                    talon.health -= dmg3;
                    if(talon.health < 0) talon.health = 0;
                    System.out.println("카시오페아 -> 탈론 "+dmg3+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                    if(talon.health <= 0) break;
                    cassiopeia.health -= dmg4;
                    if(cassiopeia.health < 0) cassiopeia.health = 0;
                    System.out.println("탈론 -> 카시오페아 "+dmg4+"의 피해 (탈론 : "+talon.health+", 카시오페아 : "+cassiopeia.health+")");
                }
                turn = 1;
            } else {
                turn++;
            }
        }
        if(talon.health > 0) {
            System.out.println("탈론 라인전 승리");
        } else {
            System.out.println("카시오페아 라인전 승리");
        }
    }
}
```

# 8번 문제
## 지문:
페이커의 현재 티어는 아이언2이다.
페이커가 랭크게임을 돌려 플래티넘 이상에 도달하게 해야한다.
승리할 확률은 50%이고, 게임 30판을 돌려야 한다.
랜덤으로 10판의 결과를 승, 패로 나누고 페이커의 티어 결과를 출력하시오.
(한 티어에서 2번을 이겨야 1단계 상승)
출력 예)
```text
게임 시작
승
승
승
패
……

페이커의 티어는 000입니다,

티어정보
아 이 언  1, 2, 3, 4
브 론 즈  1, 2, 3, 4
실    버  1, 2, 3, 4
골    드  1, 2, 3, 4
플래티넘  1, 2, 3, 4  
```

## 풀이 코드: 
```java
import java.util.Scanner;
import java.util.Random;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Random rand = new Random();
        Scanner sc = new Scanner(System.in);
        int WinStreak = 0;
        int Tier = 2;
        for(int i=0;i<10;i++) {
            int WL = rand.nextInt(2);
            if(WL == 0) {
                System.out.println("패");
            } else {
                System.out.println("승");
                WinStreak++;
                if(WinStreak == 2) {
                    Tier++;
                    WinStreak = 0;
                }
            }
        }
        int Tier_a = Tier / 5;
        String Tier_b = switch (Tier_a) {
            case 1 -> "실버";
            case 2 -> "골드";
            case 3 -> "플래티넘";
            case 4 -> "에메랄드";
            default -> "브론즈";
        };
        System.out.println("페이커의 티어는 "+Tier_b+"입니다.");
    }
}
```

# 9번 문제
## 지문:
룰루는 수제버거집을 운영하고 있다.
룰루의 가게는 장사가 매우 잘 되어 한 시간에 평균 20명의 손님이 온다.
즉, 룰루네 가게에 도착하는 손님들의 시간간격은 평균 λ =  1/20 시간인 지수분포를 따르고 있다.

룰루는 햄버거의 달인 이다. 수년간 연습을 통해 햄버거를 하나 만드는데 평균 3분이 소모된다.
정확하게 햄버거를 하나 만드는데 소비되는 시간은 2분부터 4분까지의 균등한 확률분포를 따르게 된다. 룰루는 손님을 한명씩 처리하며, 장인정신을 발휘하기 때문에 동시에 햄버거를 두개 만들지 않는다.
따라서 손님은 한줄로 서서 기다리게 된다.

예를 들어)
세명의 손님의 도착 시간 간격이 2, 2, 3이고, 룰루의 햄버거 조리 시간은 3,4,3이다.
그러면 첫번째 고객은 기다림 없이 t=2에 도착하자마자 주문하여 t=5에 햄버거를 받고 떠난다. 
두번째 고객은 t=4에 도착하여 1분을 기다린 후 t=5에 주문한 후, t=9에 떠난다. 
세번째 고객은 t=7에 도착하여 2분을 기다린후 t=9에 주문하고 t=12에 떠난다.
이 시뮬레이션에서 전체 고객의 총 기다림 시간은 4분이다.

이제, 한 시간 동안 룰루의 수제버거집에 도착하는 손님들의 총 기다린 시간을 구하는 시뮬레이션 프로그램을 작성해보시오.
(도착시간 간격과 조리시간은 소수점 두자리를 갖는 실수 난수로 발생시키시오)


## 풀이 코드:
```java
import java.util.Random;

public class Lecture0714_8 {
    public static void main(String[] args) throws InterruptedException {
        Random rand = new Random();
        float[] customers = new float[20];
        float[] cooks = new float[20];
        for(int i=0;i<20;i++) {
            cooks[i] = rand.nextFloat()*4+2;
            customers[i] = rand.nextFloat()*4+2;
        }
        int t=0, i=0, s=0;
        while(t <= 60) {
            t += customers[i];
            s += cooks[i];
            t += cooks[i];
            i++;
        }
        System.out.println(s);
    }
}
```