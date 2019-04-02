# SQL_TEST-2
--58045848 SAHAWAT SUPJAROENKOOL SEC.001

USE master
CREATE DATABASE JIB;

--1.7. SQL statements for table creations

USE JIB;
CREATE TABLE MEMBERS
(
	M_ID		VARCHAR(10)			PRIMARY KEY,
	M_NAME		VARCHAR(100)		NOT NULL,
	BYEAR		INT					NOT NULL,
	AGE		    AS (YEAR(GETDATE())-BYEAR),
	SEX			VARCHAR(2)			NULL  DEFAULT 'M'
);

CREATE TABLE EMPLOYEE
(
	E_ID		CHAR(4)			NOT NULL     PRIMARY KEY,
	E_NAME		VARCHAR(100)	NOT NULL, 
    BYEAR		INT				NOT NULL,
    AGE		    AS (YEAR(GETDATE())-BYEAR),
    SEX			VARCHAR(2)		CHECK(SEX IN ('M', 'F' )),
    SALARY		MONEY			NULL						
);

CREATE TABLE PRODUCTCPU
(
	I_ID		VARCHAR(10)		NOT NULL PRIMARY KEY,
	I_NAME		VARCHAR(50)		NOT NULL UNIQUE,
	CPU			VARCHAR(10)		CHECK(CPU IN ('AMD','INTEL')),
	SOCKET		INT				NULL DEFAULT '2000', 
	PRICE		VARCHAR(5)		NULL DEFAULT '1000'
);

CREATE TABLE SHIPMENTS
(
	M_ID	    VARCHAR(10)		NULL		FOREIGN KEY(M_ID) REFERENCES MEMBERS(M_ID),
	E_ID		CHAR(4)					    FOREIGN KEY(E_ID) REFERENCES EMPLOYEE(E_ID),
	LOCA	    VARCHAR(100)    NULL		DEFAULT 'BANGKOK',
	ORDERDATE		DATE			        DEFAULT GETDATE(),
	DATESHIP	AS (DATEADD(DAY,7,ORDERDATE))
);


CREATE TABLE SALE
(
	M_ID		VARCHAR(10)	  	FOREIGN KEY(M_ID) REFERENCES MEMBERS(M_ID),
	I_ID		VARCHAR(10)	    FOREIGN KEY(I_ID) REFERENCES PRODUCTCPU(I_ID),
	E_NAME		VARCHAR(100)	NOT NULL		,
	AGENTID		VARCHAR(50)     NULL		DEFAULT 'JIB',
	ORDERDATE		date		DEFAULT GETDATE(),
) ;


INSERT INTO MEMBERS(M_ID,M_NAME,BYEAR,SEX)
VALUES('1','NAY',2000,'F');
INSERT INTO MEMBERS(M_ID,M_NAME,BYEAR,SEX)
VALUES('2','BELL',1999,'F');
INSERT INTO MEMBERS(M_ID,M_NAME,BYEAR)
VALUES('3','JACK',1994);
INSERT INTO MEMBERS(M_ID,M_NAME,BYEAR,SEX)
VALUES('4','KWAN',1995,'M');
INSERT INTO MEMBERS(M_ID,M_NAME,BYEAR,SEX)
VALUES('5','JEY',2015,'M');
------------------------------------------------------------
INSERT INTO EMPLOYEE(E_ID,E_NAME,BYEAR,SEX,SALARY)
VALUES('E1','Mark',1965,'M',20000);
INSERT INTO EMPLOYEE(E_ID,E_NAME,BYEAR,SEX,SALARY)
VALUES('E2','Thaksin',1950,'M',20000);
INSERT INTO EMPLOYEE(E_ID,E_NAME,BYEAR,SEX,SALARY)
VALUES('E3','Payut',1954,'M',20250);
INSERT INTO EMPLOYEE(E_ID,E_NAME,BYEAR,SEX,SALARY)
VALUES('E4','Sudarat',1962,'F',20000);
INSERT INTO EMPLOYEE(E_ID,E_NAME,BYEAR,SEX,SALARY)
VALUES('E5','Thanathorn',1979,'M',20000);
---------------------------------------------------------
INSERT INTO PRODUCTCPU(I_ID,I_NAME,CPU,SOCKET,PRICE)
VALUES('9700','CORE I7','INTEL',1151,'14900');
INSERT INTO PRODUCTCPU(I_ID,I_NAME,CPU,SOCKET,PRICE)
VALUES('9980X','CORE I9','INTEL',1151,'64900');
INSERT INTO PRODUCTCPU(I_ID,I_NAME,CPU,PRICE)
VALUES('2970WX','RYZEN','AMD','47900');
INSERT INTO PRODUCTCPU(I_ID,I_NAME,CPU,SOCKET,PRICE)
VALUES('9600K','CORE I5','INTEL',1151,'9900');
INSERT INTO PRODUCTCPU(I_ID,I_NAME,CPU,PRICE)
VALUES('9600S','CORE I3','INTEL','3500');
---------------------------------------------------------
INSERT INTO SHIPMENTS(M_ID,E_ID,ORDERDATE)
VALUES('1','E2','Mar 1 2018');
INSERT INTO SHIPMENTS(M_ID,E_ID,LOCA,ORDERDATE)
VALUES('2','E2','Chonburi','1999-8-19');
INSERT INTO SHIPMENTS(M_ID,E_ID,LOCA)
VALUES('4','E1','Krabi');
INSERT INTO SHIPMENTS(M_ID,E_ID,LOCA,ORDERDATE)
VALUES('5','E5','BKK','2019-3-5');
INSERT INTO SHIPMENTS(M_ID,E_ID,LOCA,ORDERDATE)
VALUES('3','E5','Trang','2001-6-3');
---------------------------------------------------------
INSERT INTO SALE(M_ID,I_ID,E_NAME,AGENTID)
VALUES('1','9700','Mark','JIB');
INSERT INTO SALE(M_ID,I_ID,E_NAME,AGENTID,ORDERDATE)
VALUES('2','9980X','Thaksin','lazada','2005-12-30');
INSERT INTO SALE(M_ID,I_ID,E_NAME,ORDERDATE)
VALUES('3','9980X','Sudarat','2015-9-8');
INSERT INTO SALE(M_ID,I_ID,E_NAME,AGENTID,ORDERDATE)
VALUES('3','2970WX','Thaksin','lazada','1999-6-19');
INSERT INTO SALE(M_ID,I_ID,E_NAME,AGENTID,ORDERDATE)
VALUES('4','9600K','Thanathorn','Advice','2007-7-7');
---------------------------------------------------------

SELECT * FROM MEMBERS
SELECT * FROM EMPLOYEE
SELECT * FROM SHIPMENTS
SELECT * FROM SALE
SELECT * FROM PRODUCTCPU

--#1. ให้แสดงข้อมูลรหัสพนักงาน ชื่อพนักงาน และเงินเดือนของพนักงานทั้งหมด
SELECT E_NAME,SALARY FROM EMPLOYEE;

--#2. ให้แสดงข้อมูลรหัสพนักงาน ชื่อพนักงาน และเงินเดือนของพนักงานที่ได้เงินเดือนมากกว่า20000
SELECT E_NAME,SALARY FROM EMPLOYEE  WHERE SALARY > 20000;

--#3. ให้แสดง สมาชิกที่อายุต่ำกว่า 20
SELECT M_NAME,AGE FROM MEMBERS WHERE AGE <20 ;

--#4. ให้แสดง สินค้าที่แพงกว่า50000 
SELECT I_NAME,CPU,PRICE FROM PRODUCTCPU WHERE PRICE >50000 ;

--#5. ให้แสดง สินค้าที่ส่งก่อนปี2019
SELECT * FROM SHIPMENTS WHERE DATESHIP < '01-01-2019'


