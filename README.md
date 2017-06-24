package com.lizhenbo.observerdemo;

import java.util.ArrayList;
/**
 * 具体的通知类Hr(Boss,项目经理的具体类不在赘述)
 * @author LIZHENBO
 */
public class HrSubject implements Subject{
	
	private String name;//名字非必要,为了方便理解加上的
	
	private ArrayList<Observer> observers=new ArrayList<Observer>();
	
	public HrSubject(String name) {
		super();
		this.name = name;
	}

	@Override
	public void Attach(Observer observer) {
		observers.add(observer);
	}

	@Override
	public void Detach(Observer observer) {
		observers.remove(observer);
	}

	@Override
	public void NotifyObserver() {
		for (Observer observer : observers) {
			System.out.println("我是Hr:"+name+",通知您来面试!!");
			observer.Update();
		}
	}
}
package com.lizhenbo.observerdemo;
/**
 * 观察者的接口,所有具体的观察者都必须实现该接口
 * 暂且可以比作,观察者(所有具体的观察者(社招人员,校招人员...)接受到通知后要更新状态都必须实现该接口)
 * @author LIZHENBO
 *
 */
public interface Observer {
	//订阅者收到通知后更新状态
	void Update();
}
package com.lizhenbo.observerdemo;

public class ObserverTest {

	public static void main(String[] args) {
		//创建一个名字为马云的Hr的通知者
		HrSubject hr=new HrSubject("马云");
		//创建了三个校招人员的订阅者
		StudentObserver student01=new StudentObserver("李振博");
		StudentObserver student02=new StudentObserver("李明夏");
		StudentObserver student03=new StudentObserver("李明月");
		//添加和移除订阅者
		hr.Attach(student01);
		hr.Attach(student02);
		hr.Attach(student03);
		hr.Detach(student03);
		//通知已经添加的所有订阅者
		hr.NotifyObserver();
	}
}
package com.lizhenbo.observerdemo;
/**
 * 具体的观察者Student(订阅者),社招人员的具体类不在赘述
 * @author LIZHENBO
 */
public class StudentObserver implements Observer{

	private String name;//名字非必要,为了方便理解加上的
	
	public StudentObserver(String name) {
		super();
		this.name = name;
	}

	@Override
	public void Update() {
		System.out.println("我是"+name+"已接收到面试通知,一定准时到达!!");
	}

}
package com.lizhenbo.observerdemo;
/**
 * 通知者的接口,所有具体的通知者,必须实现该接口
 * 暂且可以比作,面试通知的功能(HR,项目经理,老板...谁需要这个功能谁就实现这个接口)
 * @author LIZHENBO
 */
public interface Subject {
	//添加订阅者
	void Attach(Observer observer);
	//移除订阅者
	void Detach(Observer observer);
	//通知订阅者
	void NotifyObserver();
}

Hrsubject：该模块为具体主题角色，是具体的被观察者，它将有关状态存入通过StudentObserver创建的具体观察者中，在它的内部状态改变时，给登记过的发出通知。
Observer：该模块为抽象观察者，为所有具体的观察者定义一个接口，在得到主题的通知时更新自己。
StudentObserver：该模块为具体观察者，实现抽象观察者所要求的更新接口，使自身的状态与主题的状态相协调。
Subject：该角色为被观察者，可以增加删除观察者对象。
ObserverTest：为Client。


