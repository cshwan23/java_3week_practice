# java_3week_practice
3주차 복습



//문법이 바뀌면 어느줄에서 에러가 나는가? - 시험문제(단어들을 문법을 바꿔봐야함)
package com.eee.erp;

//******************************************
// 계좌 정보를 관리하는 [Account 클래스] 선언
//******************************************
class Account{
	
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 속성변수선언.
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	String accountNo;		   // 계좌번호
	int remainAmount = 9000;   // 잔액(남아있는 양) 
	
	
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 생성자 오버로딩. 같은 이름 생성자 두개이상 만들때 => 생성자 오버로딩 
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	public Account() { }   
	public Account( String accountNo, int remainAmount ) {
		this.accountNo = accountNo;
		this.remainAmount = remainAmount;
	}
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 메소드 선언. 
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	
	// 입금하는 메소드 선언
	public void deposit(int inputAmount) {
		// 속성변수 remainAmount에 매개변수 inputAmount로 입금액을 누적 
		remainAmount = remainAmount + inputAmount;
		System.out.print("\n[입금발생]=> [입금액]:" + inputAmount 
				+ "[잔고]:" + remainAmount + "\n");
		
	}
	
	// 출금하는 메소드 선언	
	public void withdraw(int outputAmount) {
		// 만약 출금액이 잔액보다 같거나 적으면 
		if (remainAmount >= outputAmount) {
			//속성변수 remainAmount에 출금액을 뺀다. 
			remainAmount = remainAmount - outputAmount;
		// 도스창에 출금내역 출력
		System.out.print("\n[출금발생]=> [출금액]:"+outputAmount+"[잔고]:"+remainAmount+"\n");
		// 만약 출금액이 잔액보다 크면
		}else{
		// 경고문구 출력
		System.out.print("\n[출금발생]=> [출금실패]: 출금액이 잔액보다 큽니다.");
		}
		
	}
	
}

//******************************************
// 체크카드 정보를 관리하는 [CheckCard 클래스] 선언
	// Account 클래스를 슈퍼 클래스로 삼고 있다.
//******************************************
class CheckCard extends Account {
	// account 를 객체화 시켯엇는데
	// 자신만 객체화 시키면 부모걸(Account클래스) 갖고올 수 있다.
	
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 속성변수선언.
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	public String cardNo; 			//체크카드 번호
	private int totPaymentAmount;	//체크카드 총지출액

	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 생성자 선언.(클래스 이름과 같다)  // 여기서부터 어려워진다****
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	public CheckCard() { }   // <---{안에super() 가 숨어있다. } 첫줄에 super가 나와야하는데 안넣으면 **자동으로 들어간다.
	public CheckCard(String accountNo, int remainAmount, String cardNo) {

	// super()-> 뭔뜻이야.  // 엄마쪽으로 집어던진다.
	// 부모 클래스의 생성자 호출	
	super(accountNo, remainAmount);
	// 매개변수 cardNo 안의 데이터를 속성변수 cardNo에 저장 
	this.cardNo = cardNo;
	
	 }
	
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
	// 메소드 선언. 
	//ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ 
	// 체크카드 지출 메소드 선언, 즉 카드를 긁었을 때 호출되는 메소드 
	// 카드를 긁자마자 이 메소드 호출.  매개변수는 긁은 금액이 들어온다 
	public void cardPayment(int paymentAmount) {
		// 이 안에 잔액에 대한 변수 없다. 엄마클래스가 갖고있다. (Account 클래스)
		
		// 만약 카드 지출액이 잔액보다 같거나 적으면
		
		// remainAmount 는 엄마쪽 변수인데 객체생성없이 사용 가능하다 extends 했기 때문에.
		// 만약 카드 지출액이 잔액보다 크면
		if (remainAmount >= paymentAmount) {
			//카드를 계속 긁으면 카드 긁은 누적도 보고싶다.
			
			//카드 지출액 누적
			totPaymentAmount = totPaymentAmount + paymentAmount;
			//계좌 잔액에서 빼기
	    	remainAmount = remainAmount - paymentAmount;
			//도스창에 카드 지출내역 출력
			System.out.print("\n[체크카드지출발생]=> [카드지출액]:"+paymentAmount
				+" [잔고]:"+remainAmount+" [카드총지출액]"+totPaymentAmount+"\n");
		}
		// 만약 카드 지출액이 잔액보다 크면
		else {
			System.out.print( "\n[체크카드지출발생] => [체크카드지출실패]:지출금액이 잔액보다 큽니다."+"\n");
		}

	}

}

//******************************************
// CheckCard 클래스를 객체화 하고 메소드를 호출하기 CheckCardExe 클래스 선언  
//******************************************
public class CheckCardExe {
	
	public static void main(String[] args) {
		
		//+++++++++++++++++++++++++++++++++++++++++++++++
		//CheckCard 클래스를 객체화 하고 객체의 메위주를 card 변수 저장
		//+++++++++++++++++++++++++++++++++++++++++++++++
		CheckCard card = new CheckCard("112233", 900000, "898989");
		
			//	<1>객체 참조 변수 card 선언
			//  <2>수입한 클래스 중에 생성자 CheckCard( 문자,정수,문자) 를 
			// 			소유한 클래스를 찾아서 있으면
			// 			CheckCard 클래스를 메모리 공간에 올려 객체화 시킨다.
			//		    (부모가 있으면 부모도 같이 따라 올라간다)
			// 			이때 CheckCard 클래스의 조상 클래스도 같이 모두 객체화 된다.
			//			여기서 CheckCard 클래스의 조상 클래스는 Account 클래스가 된다.
			// 			결국 CheckCard 클래스의 조상 클래스는 Account 클래스이다..
			// 			결국 CheckCard 객체와 Account 객체가 생성된 것이다.
			// 	<3>CheckCard 객체의 생성자를 CheckCard("112233", 900000, "898989")로 호출한다.
			//  <4>CheckCard 객체의 메모리 위치 주소값을 리턴하여 변수 card 에 저장.
	
		
		//+++++++++++++++++++++++++++++++++++++++++++++++
		// 카드를 긁어서 cardPayment 메소드를 호출하기 
		//+++++++++++++++++++++++++++++++++++++++++++++++
		card.cardPayment(70000);  // 긁기 성공
//		card.cardPayment(300000); // 긁기 성공 
//		card.cardPayment(600000); // 긁기 실패 
		

	}

}


/*
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
1문제 : int remainAmount; 을 private int remainAmount; 로 수정하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
  int remainAmount 를 private int remainAmount로 수정하면???
  default 인데 이건 부모클래스의 속성변수라 아래 자식클래스에서 호출이 불가능하므로 에러가 뜬다 
  어디에서 에러가 뜨냐? 
: 73 77     <---- 생성자에선 에러가 발생 하지 않는다. 95 101 104
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
2문제 : CheckCard 클래스에서 super( accountNo, remainAmount);를 삭제하면?	
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
 CheckCard 클래스에서 super( accountNo remainAmount)를 삭제하면
 부모클래스의 변수를 상속받고 호출하는 생성자가 없으므로 
 그위에 부모의 같은 속성변수의 이름의 생성자를 호출 불가능 하다 
:73 95 101 104
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제3 : super(accountNo, remainAmount); this.cardNo = cardNo; 를	
		this.cardNo = cardNo; super(accountNo, remainAmount)로 바꾸면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제4 : CheckCard 클래스에서 public CheckCard(){} 를 삭제하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제5 : Account 클래스에서 public Account(){}를 삭제하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제6 : CheckCard card = new CheckCard("123-456-78-9", 90000, "456-78-10-2"); 를
	   Account card = new CheckCard("123-456-78-9", 90000, "456-78-10-2");로 수정하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제6-1 : card.cardPayment(70000); 부문에서 발생하는 에러를 없앨 수 있다면 
	  card.cardPayment(70000); 를 어떻게 수정하나?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ









 * 
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
1문제 : int remainAmount; 을 private int remainAmount; 로 수정하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> 에러 발생. CheckCard 클래스이ㅡ 아래 코딩 부분에서 에러 발생.
=> remainAmount 속성변수 호출 지점에서 에러 발생.
		=> if (remainAmount >= paymentAmount){
		=> remainAmount = remainAmount - paymentAmount;
		=> System.out.print("\n\n [체크카드지출발생]=> [카드지출액]:"+paymentAmount
					+" [잔고]:"+remainAmount+" [카드총지출액]"+totPaymentAmount+"\n");
		
	
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
2문제 : CheckCard 클래스에서 super( accountNo, remainAmount);를 삭제하면?	
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> 에러 없음.
=> super( accountNo, remainAmount); 을 삭제하면 컴파일 할 때 super( ); 를 넣어준다.
   super( ) 는 부모클래스의 생성자 ( ) 를 호출하라는 얘긴데
   현재 슈퍼클래스에는 호출할 Account( )라는 생성자가 있으므로 아무일 없다.
   만약 부모 클래스에 Account( ) 라는 생성자가 없다면 에러가 발생한다.



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제3 : super(accountNo, remainAmount); this.cardNo = cardNo; 를	
		this.cardNo = cardNo; super(accountNo, remainAmount)로 바꾸면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> 에러 발생
=> 자식 클래스 생성자 안에서 호출되는 super(~) 는 반드시 첫줄에 나와야 한다.
   자바의 지극한 효도심....눈물난다.
   
   super 위에 코딩이 없어야한다.
   밑에 super가 나오면...
   super에서 에러가 나면. "부모쪽은 초기화가 안돼". 부모가 에러가 나면 첫줄에 나와야 되는거 아니냐 이거지.
   무조건 에러나더라도 부모부터 안정화 시키고 에러내라 이얘기다.



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제4 : CheckCard 클래스에서 public CheckCard(){} 를 삭제하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> 아무일 없음
=> 만약 서브클래스를 객체 생성할 때 new CheckCard( )라는 코딩이 있었다면 에러발생.
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ






ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제5 : Account 클래스에서 public Account(){}를 삭제하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> 에러 발생
=> 서브클래스의 생성자 public CheckCard( ) { } 안의 첫줄에는 "super( )"가 자동 삽입된다.
   super( )는 슈퍼클래스의 생성자 Account( ) { }를 호출하라는 얘긴데
   삭제했으므로 호출할 부모 생성자가 없어 에러 발생.



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제6 : CheckCard card = new CheckCard("123-456-78-9", 90000, "456-78-10-2"); 를
	   Account card = new CheckCard("123-456-78-9", 90000, "456-78-10-2");로 수정하면?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
// 객참변수는 부모걸 썻는데 고유멤버 메소드 호출 불가능.(고유멤버 =>자기가갖고있는 그안에서만 선언된 고유속성변수 ) 
 * 고유멤버가 아닌건 자기쪽 오버라이드된 메소드 거나  부모쪽 선언된 변수
=> 에러 발생
=> 		card.cardPayment(70000);  에서 에러 발생
		card.cardPayment(300000); 에서 에러 발생
		card.cardPayment(600000); 에서 에러 발생
		
=> 슈퍼클래스명  객체참조변수  = new  서브클래스명(~) 선언 시
   서브클래스의 고유 멤버는 호출불가능.
   
=> 객참변수의 자료형을 부모형으로 쓰는 이유
   	  자식클래스가 2개 이상일 때 어느 자식 클래스가 객체화 될지 모를 경우이다.
   	  어느 자식이 객체화 될지 모르는 상태에서 자식의 고유 메소드를 호출하는 것은 모순이다.
   	  그러므로 모든 자식이 호출할 수 있는 오버라이딩한 메소드나 부모의 메소드만 호출 가능하도록 허락하는 것이다.
   		
=>에러가 안나게 하려면
=>		((CheckCard)card).cardPayment(70000);  
		((CheckCard)card).cardPayment(300000); 
		((CheckCard)card).cardPayment(600000); 
 
 	다시 자식으로 돌려놓는다 -> cast 연산자 를 사용 card 를 CheckCard 자료형으로 형변환.
 	부모 자료형을 자식 자료형으로 끌어내릴 수 있다. 캐스트 연산자로.
 
 
 ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
문제6-1 : card.cardPayment(70000); 부문에서 발생하는 에러를 없앨 수 있다면 
	  card.cardPayment(70000); 를 어떻게 수정하나?
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
=> ((CheckCard)card).cardPayment(70000); 

=>  다시 자식으로 돌려놓는다 -> cast 연산자 를 사용 card 를 CheckCard 자료형으로 형변환.
 	부모 자료형을 자식 자료형으로 끌어내릴 수 있다. 캐스트 연산자로.
 
 
 
 */


