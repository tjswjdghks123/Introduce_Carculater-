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

