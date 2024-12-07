Department.java


package com.klef.jfsd.exam;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "department")
public class Department {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int departmentId;
    private String name;
    private String location;
    private String hodName;
	public int getDepartmentId() {
		return departmentId;
	}
	public void setDepartmentId(int departmentId) {
		this.departmentId = departmentId;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getLocation() {
		return location;
	}
	public void setLocation(String location) {
		this.location = location;
	}
	public String getHodName() {
		return hodName;
	}
	public void setHodName(String hodName) {
		this.hodName = hodName;
	}

}





ClientDemo.java


package com.klef.jfsd.exam;

import java.util.Scanner;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class ClientDemo {
    public static void main(String[] args) {
        Configuration cfg = new Configuration().configure("hibernate.cfg.xml");
        SessionFactory factory = cfg.buildSessionFactory();
        Session session = factory.openSession();
        Transaction tx = session.beginTransaction();

        // Insert records manually
        Department dept1 = new Department();
        dept1.setName("Computer Science");
        dept1.setLocation("Hyderabad");
        dept1.setHodName("Dr. Smith");

        Department dept2 = new Department();
        dept2.setName("Electronics");
        dept2.setLocation("Chennai");
        dept2.setHodName("Prof. Patel");
        tx.commit();

        // Delete records using HQL with positional parameters
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the Department ID to delete: ");
        int departmentIdToDelete = scanner.nextInt();

        tx = session.beginTransaction();
        String hql = "DELETE FROM Department WHERE departmentId = ?";
        int result = session.createQuery(hql)
                .setParameter(1, departmentIdToDelete)
                .executeUpdate();
        tx.commit();

        System.out.println(result + " record(s) deleted.");

        session.close();
        factory.close();
        scanner.close();
    }
}






Xml file



<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
	"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
	"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

	<hibernate-configuration>
	<session-factory>
	
	<!--  Connection Properties  -->
<property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>
<property name="connection.url">jdbc:mysql://localhost:3306/hibernate21</property>
<property name="connection.user">root</property>
<property name="connection.password">Charan@30M</property>

<!--  Hibernate Properties  -->
<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
<property name="hibernate.hbm2ddl.auto">update</property>
<property name="hibernate.show_sql">true</property>
	
    <mapping class="com.klef.jsfd.exam.Department"/>

</session-factory>
	
	</hibernate-configuration>
