# Introduce_Carculater-
## 계산기 만들기 과제 

 저는 기본적인 사칙연산이 수행되는 계산기를 구상했습니다.

 [참고자료](https://www.yes24.com/Product/Goods/95717011)
 [참고사이트](https://chatgpt.com/)

* 계산기의 틀을 구상
  * 무슨 레이아웃으로 할까?
  * 기본적으로 윈도우계산기를 보면 위에 숫자가 입력되고 아래에 키패드가 있다.
  * JFrame을 클래스에 상속받게 하고 기본 레이아웃인 Border로 구상.
 
```java
	TestCalculater() {
		
		setTitle("계산기");
		setLayout(new BorderLayout(10,10));
		
		showNorth();
	
		setSize(320,670);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		this.setIconImage(getIconImage());
		setVisible(true);
		
	}
	
	void showNorth() {
		JTextField t = new JTextField("0",100);
		add(t, BorderLayout.NORTH);
		
		
	}
	
	
	
	public static void main(String[] args) {
		new TestCalculater();
	}
}
```
  * 기본적인 틀 완성.
  * 다음은 버튼을 넣고 꾸미는 것
```java
void showCenter() {
        String[][] Text = { { " ", " ", " ", "X" }, { "7", "8", "9", "x" }, { "4", "5", "6", "-" },
                { "1", "2", "3", "+" }, { " ", "0", ".", "=" } };
        p = new JPanel(new GridLayout(5, 5, 2, 2));
        for (int i = 0; i < Text.length; i++) {
            for (int j = 0; j < Text[i].length; j++) {
                JButton bt = new JButton(Text[i][j]);
                bt.setBackground(Color.WHITE);
```
기본적인 계산기형식의 틀을 구성
2중 for문을 사용하여 텍스트를 넣어주고 버튼도 넣어줌

이제는 연산을 구상해야함.
일단 구상해본것이 카드레이아웃을 이용

```java
	// 첫 번째 카드: t1 텍스트 필드를 포함하는 패널
		JPanel firstCard1 = new JPanel();
		t1 = new JTextField("0", 27);
		t1.setHorizontalAlignment(JTextField.RIGHT); // 숫자 오른쪽정렬
		firstCard1.add(t1);
		cardPanel.add(firstCard1, "Cd1");
		// 두 번째 카드: t2 텍스트 필드를 포함하는 패널
		JPanel firstCard2 = new JPanel();
		t2 = new JTextField("0", 27);
		t2.setHorizontalAlignment(JTextField.RIGHT);
		firstCard2.add(t2);
		cardPanel.add(firstCard2, "Cd2");
		// 세 번째 카드: t3 텍스트 필드를 포함하는 패널
		JPanel firstCard3 = new JPanel();
		t3 = new JTextField("0", 27);
		t3.setHorizontalAlignment(JTextField.RIGHT);
		firstCard3.add(t3);
		cardPanel.add(firstCard3, "C3");
```
첫 번째 카드에는 연산값입력 사칙연산할 연산자아무거나를 입력하면 다음 카드레이아웃으로 바뀌는 형식으로 구상 



버튼이 눌리면서 처리를 하기때문에 버튼이벤트처리로
추가로 조건연산자를 사용해서 경우의 수를 지정

```java
bt.setActionCommand(Text[i][j]);
		        bt.addActionListener(e -> {
		            JTextField currentField = t1.isShowing() ? t1 : t2; // 조건연산자 활용 현재 카드에 따라 필드 선택
		            String currentText = currentField.getText();
		            String c = e.getActionCommand(); // 버튼값을 받아서 스트링 c에 넣어줌

```
다음은 사칙연산
```java
 } else if (c.equals("+") || c.equals("-") || c.equals("x") || c.equals("÷")) { // 연산자 버튼이 눌릴 때
		                if (t3.isShowing()) { // 이전에 한 번 결과가 왔다면.
		                    mix1 = t3.getText(); // t3의 결과를 mix1에 저장
		                    t1.setText(mix1); // t1에도 결과 표시
		                    cd.show(cardPanel, "Cd1"); // 첫 번째 카드로 전환
```
첫 연산 이 사칙연산중 하나인경우 값을 넣어주는 코드를 구상

# 여러변수와 오류를 수정한 최종코드
```java
package pkg;

import java.awt.BorderLayout;
import java.awt.CardLayout;
import java.awt.Color;
import java.awt.GridLayout;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JTextField;

public class TestCalculater extends JFrame {

	CardLayout cd;
	JPanel cardPanel;
	JTextField t1, t2, t3; // t1: 첫 번째 숫자, t2: 두 번째 숫자, t3: 결과
	JPanel p;
	String mix1, mix2, result;// 연산에 사용할 변수
	String currentOperation; // 현재 연산자를 저장할 변수

	TestCalculater() {
		setTitle("계산기");
		setLayout(new BorderLayout(10, 10));

		cd = new CardLayout();
		cardPanel = new JPanel(cd);

		// 첫번째 카드 t1를 포함하는 패널
		JPanel firstCard1 = new JPanel();
		t1 = new JTextField("0", 27);
		t1.setHorizontalAlignment(JTextField.RIGHT); // 숫자 오른쪽정렬하는 메소드
		firstCard1.add(t1);
		cardPanel.add(firstCard1, "Cd1");

		// 두번째 카드 t1를 포함하는 패널
		JPanel firstCard2 = new JPanel();
		t2 = new JTextField("0", 27);
		t2.setHorizontalAlignment(JTextField.RIGHT);
		firstCard2.add(t2);
		cardPanel.add(firstCard2, "Cd2");

		// 세번째 카드 t1를 포함하는 패널
		JPanel firstCard3 = new JPanel();
		t3 = new JTextField("0", 27);
		t3.setHorizontalAlignment(JTextField.RIGHT);
		firstCard3.add(t3);
		cardPanel.add(firstCard3, "Cd3");

		add(cardPanel, BorderLayout.CENTER); // 카드 패널 추가

		String[][] Text = { { "10", "11", "12", "C" }, { "7", "8", "9", "x" }, { "4", "5", "6", "-" },
				{ "1", "2", "3", "+" }, { "±", "0", "÷", "=" } };

		p = new JPanel(new GridLayout(5, 4, 2, 2)); // 5x4 버튼 배치

		for (int i = 0; i < Text.length; i++) {
		    for (int j = 0; j < Text[i].length; j++) {
		        JButton bt = new JButton(Text[i][j]);
		        bt.setBackground(Color.WHITE);

		        if (j == 0 || j == 1 || j == 2) { // 버튼의 색을 입혀줌
		            bt.setForeground(Color.BLUE);
		        } else if (j == 3 || j == 4) {
		            bt.setForeground(Color.RED);
		        }

		        bt.setActionCommand(Text[i][j]);
		        bt.addActionListener(e -> {
		            JTextField currentField = t1.isShowing() ? t1 : t2; // 조건연산자 활용 현재 카드에 따라 필드 선택
		            String currentText = currentField.getText();
		            String c = e.getActionCommand(); // 버튼값을 받아서 스트링 c에 넣어줌

		            if (c.equals("=")) { // 결과 버튼 클릭 시
		                mix2 = t2.getText(); // 두 번째 숫자 저장
		                int result = 0; //결과를 담은 변수

		                if (currentOperation != null) { //현제값이 빈 값이 아닐때 
		                    if (currentOperation.equals("+")) {
		                        result = Integer.parseInt(mix1) + Integer.parseInt(mix2); //문자열을 인트로 바꿔서 연산
		                    } else if (currentOperation.equals("-")) {
		                        result = Integer.parseInt(mix1) - Integer.parseInt(mix2);
		                    } else if (currentOperation.equals("x")) {
		                        result = Integer.parseInt(mix1) * Integer.parseInt(mix2);
		                    } else if (currentOperation.equals("÷")) {
		                        result = Integer.parseInt(mix1) / Integer.parseInt(mix2);
		                    }
		                    t3.setText(String.valueOf(result)); // 결과 표시
		                    mix1 = String.valueOf(result);
		                    cd.show(cardPanel, "Cd3"); // 결과 카드로 전환
		                }
		            } else if (c.equals("+") || c.equals("-") || c.equals("x") || c.equals("÷")) { // 연산자 버튼이 눌릴 때
		                if (t3.isShowing()) { // 이전에 한 번 결과가 왔다면.
		                    mix1 = t3.getText(); // t3의 결과를 mix1에 저장
		                    t1.setText(mix1); // t1에도 결과 표시
		                    cd.show(cardPanel, "Cd1"); // 첫 번째 카드로 전환
		                } else {
		                    mix1 = t1.getText(); // 첫 번째 숫자 저장
		                }
		                currentOperation = c; // 현재 연산자 저장
		                cd.show(cardPanel, "Cd2"); // 두 번째 카드로 전환
		                t2.setText("0"); // 두 번째 입력 필드 초기화
		            } else if (c.equals("C")) { // 초기화 버튼
		                t1.setText("0"); // 첫 번째 필드 초기화
		                t2.setText("0"); // 두 번째 필드 초기화
		                t3.setText("0"); // 결과 필드 초기화
		                cd.show(cardPanel, "Cd1");
		                currentOperation = null; // 초기화 후 연산자도 초기화
		                
		            } else if (c.equals("±")) { // ± 버튼 클릭 시 부호 전환
		                JTextField visibleField = t1.isShowing() ? t1 : (t2.isShowing() ? t2 : t3); // 현재 보이는 필드 선택
		                int cV = Integer.parseInt(visibleField.getText());
		                visibleField.setText(String.valueOf(-cV)); // 부호를 반대로 
		            } else { // 숫자 버튼 클릭
		                if (currentText.equals("0")) {
		                    currentField.setText(c); // 0일 경우 숫자 입력
		                } else {
		                    currentField.setText(currentText + c); // 기존 숫자에 추가
		                }
		            }
		        });

		        p.add(bt); // 버튼을 패널에 추가
		    }
		}


		add(p, BorderLayout.SOUTH); // 버튼 패널 추가

		setSize(320, 230);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setVisible(true);
	}

	public static void main(String[] args) {
		new TestCalculater();
	}
}

```


