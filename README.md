# **Importing files to SQL**

In this repository, an approach was described as How to import files into SQL database by file streaming technique

First of all, it is necessary to enable the file streaming in SQL server. 
So in Sql server configuration manager, follow steps as shown in the pictures below

## 👉 Step 1: 
 > ![Enabling0](https://user-images.githubusercontent.com/45565026/196166536-4059e717-5673-4b3d-8538-eeda8ed50721.png)

## 👉 Step 2:  
 > ![Enabling1](https://user-images.githubusercontent.com/45565026/196167752-dafde568-00d2-47ae-b718-b10778e8e736.png)

## 👉 Step 3:  
 > ![Enabling2](https://user-images.githubusercontent.com/45565026/196167900-b103a3b7-9f02-470e-9bc5-3e11413ed996.png)

## 👉 Step 4:  
 > ![Enabling3](https://user-images.githubusercontent.com/45565026/196167958-4b7c397c-9862-4599-80e5-9132a4e6b542.png)
 
## 👉 Step 5:  
 Then in management studio 
 > ![Enabling4](https://user-images.githubusercontent.com/45565026/196167982-c825f474-c760-4dd0-862c-c1daae6c83fb.png)
 
## 👉 Step 6:  
 > ![Enabling5](https://user-images.githubusercontent.com/45565026/196167999-5ed54d1e-b675-42ac-a9d1-bd474d0cb0b0.png)
 
Second, it is necessary to config the database so in the desired database properties set config below

## 👉 Step 1: 
 > ![ConfigDB0](https://user-images.githubusercontent.com/45565026/196172639-50f2c9c4-bb78-46af-bcbe-ddb84d441766.png)

## 👉 Step 2: Adding file group
 > ![ConfigDB1](https://user-images.githubusercontent.com/45565026/196172781-c2f58858-b7f1-4802-8518-ba95a6f02ef7.png)

## 👉 Step 3: 
 > ![ConfigDB3](https://user-images.githubusercontent.com/45565026/196172970-dcb1e1a0-ef3f-40a2-835a-a29cf82a0850.png)

## 👉 Step 4: Adding DB file
 > ![ConfigDB4](https://user-images.githubusercontent.com/45565026/196173161-9f5b5ef3-8f52-4212-bf27-e90928160513.png)

Now by the means of script below a table should be created. Note that the name of FILESTREAM_ON should be the name of the file group was specified in previews steps --> [DocFileGroup]
```
CREATE TABLE [dbo].[FILESTREAM_Documents](
  [DocumentID] [uniqueidentifier] ROWGUIDCOL  NOT NULL,
  [DocumentName] [varchar](128) NULL,
  [DocumentType] [varchar](10) NULL,
  [DocumentFS] [varbinary](max) FILESTREAM  NOT NULL,
UNIQUE NONCLUSTERED 
(
  [DocumentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY] FILESTREAM_ON [DocFileGroup]
GO

```


