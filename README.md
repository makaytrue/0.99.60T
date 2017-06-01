  
1. Description of Mu Server
A.	JoinServer
i.	For account authentication and (Billing system when commercial service)
B.	GameServer
i.	Connected to client, actually the game applied server
C.	ConnectServer
i.	For Client Update(version) management and game server list management 
D.	DataServer
i.	For game character information and DB save/load 
E.	ExDB
i.	For Guild and friend management DB
F.	ChatServer
i.	Connected to client to control chat during users
G.	RankingServer
i.	For ranking of Devil Square and Blood Castle
H.	EventServer
i.	For gift management from event
I.	WzFsGate
i.	Data management of game server
 
2.	Installation of Mu Server System sequence (For each server installation, refer to each server installation below this topic)
1> . Execute WzFsGate, then check it works or not
	Refer to installation of WzFsGate
2> . Install Authentic DB and Authentic Server
	Refer to installation of JoinServer
3> . Install Connect server list and Connect server.
	Refer to installation of ConnectServer
4> . Install Game Data.
	Refer to installation of DataServer, ExDB
5> . Install GameDB, Data Server, and EXDB.
	Refer to installation of DataServer, ExDB
6> . Install Chat Server.
	Refer to installation of ChatServer
7> . Install EventDB and EventServer.
	Refer to installation of EventServer
8> . Install RankingDB and Rangking Server.
	Refer to installation of RankingServer
9> . Install Game Server.
	Refer to installation of GameServer
10> . Perform Map Server divided (For Castle Siege)
	Refer to appendix of Castle Siege (not included in this document)
11> . Execute them, following by the sequence
	File Transfer Server : WzFsGate.exe
	Authentic Server : JoinServer.exe
	Connect Server : CS.exe
	Data Server : DataServer.exe
	EXDB : ExDB.exe
	Chat Server : ChatServer.exe
	Ranking Server, Event Server : MU_RANKING_DB_SERVER.exe, WZ_MU2003_EVENT_SERVER.exe
	Game Server : GameServer.exe
 
3.	Installation JoinServer / DB 
A.	Execute MS-SQL Enterprise Manager (EM)
B.	Execute Query Analyzer
C.	Check the running of SQL Server Agent
D.	Making Me_MuOnline DB
i.	DB for user’s account information.
ii.	Choose master DB
iii.	In Query Analyzer, open \\DBScript\JoinServer\Me_Muonline Me_Muonline_CreateDB.sql, Me_MuOnline.sql , and execute it
1.	File Structure
\\DbScript\Me_Muonline\Default_ODBC.txt
\\DbScript\Me_Muonline\Me_Muonline.sql
\\DbScript\Me_Muonline\Me_Muonline_CreateDB.sql

iv.	Check if Me_MuOnline DB is created and Table, SP are created also.
v.	Refer to DB related document for the Table and SP

E.	Install MD5 for JoinDB to make account encryption. MD5 module is extended save procedure type, so that it can be used on SQL server directly.
i.	Host where JoinDB in SQL server installed, open C:\Program Files\Microsoft SQL Server\MSSQL\Binn\ folder, and then search a patch file named \\MD5_EXSP_DLL\WZ_MD5_MOD.dll, then copy.
1.	File Structure
\\MD5_EXSP_DLL\WZ_MD5_MOD.dll : Encryption extended save procedure DLL
\\MD5_EXSP_DLL\UserDefinedFunction.sql : user definition function which help using Encryption of Extended save procedure
\\MD5_EXSP_DLL\readme.txt : Installation of Encryption of extended save procedure

ii.	Refer to file \\MD5_EXSP_DLL\readme.txt, install it.
iii.	Caution : You MUST install user definition function of \\MD5_EXSP_DLL\UserDefinedFunction.sql on Me_Muonline DB above. (NEVER INSTALL IT ON master DB)

 
F.	Installation of MuLog DB
i.	DB for gamer user connect/disconnect and game time involved information
ii.	Execute Query Analyzer
iii.	Choose master DB
iv.	In Query Analyzer, open the folder \\DBScript\MuLog 폴더내에 MuLog_CreateDB.sql, MuLogCreate.sql, and then execute it.
1.	File Structure
\\DbScript\MuLog\Default_ODBC.txt
\\DbScript\MuLog\MuLog_CreateDB.sql
\\DbScript\MuLog\MuLogSchedule.sql

2.	To execute it, SQL Agent must be running (!!!.IMPORTANT)
v.	Check the creation of MuLog DB, and schedule is running properly
vi.	Table is made on 23:00 everyday, for tomorrow one
G.	Create administrator account
i.	Create “MuOnlineAdmin” DataBase account
 
H.	Installation of JoinServer
i.	File Structure
\\JoinServer\JoinServer.exe : Authentic server execution file
\\JoinServer\Log : Folder where Authentic server log is saved (Folder must be made before the performance!)

ii.	ODBC Setup
1.	Me_MuOnline DB ODBC Setup
a.	Refer to \\DBScript\JoinServer\Me_Muonline\Default_ODBC.txt 
2.	MuLog DB ODBC Setup
a.	Refer to \\DBScript\JoinServer\MuLog\Default_ODBC.txt

iii.	Installation of JoinServer
1.	Program for user authentication and billing process
2.	Make shortcut of JoinServer.exe and extention
a.	/p : JoinServer port (default is 55970)
b.	/ca : ConnectServer IP (required)
c.	/cp : ConnectServer의 Port (default is 55557)
d.	You must put /ca(ConnectServer IP) all the time
e.	Example)
 “C:\MuOnline\JoinServer\JoinServer.exe /ca172.16.100.3”

 
4.	Installation of DataServer, ExDB, DB
A.	Execute EM
B.	Execute Query Analyzer
C.	Creation of MuOnline DB
i.	DB for Game data management
ii.	Choose master DB
iii.	On Query Analyzer, open the folder \\DBScript\MuOnline, and execute MuOnline_CreateDB.sql, MuOnline.sql
1.	File Structure
\\DBScript\MuOnline\Default_ODBC.txt
\\DBScript\MuOnline\MuOnline_CreateDB.sql
\\DBScript\MuOnline\MuOnline.sql
\\DBScript\MuOnline\GameServer_Init_Data.sql
			
iv.	Check MuOnline DB is created and Table, SP are created
v.	Refer to related document for Table and SP in DB
vi.	Check if the number of GameServerInfo table is 0, 0, 0 as initial -> Put it directly through EM, or use the query in GameServer_Init_Data.sql by the execution of Query Analyzer

D.	Create Administrator account
i.	“Admin” DataBase account creation -> Refer to \\DBScript\MuOnline\Default_ODBC.txt


 
E.	Installation of DataServer, ExDB
i.	ODBC Setup
1.	Refer to \\DBScript\JoinServer\MuOnline\Default_ODBC.txt
ii.	Installation of DataServer
1.	File Structure
\\DataServer\DataServer.exe : Data Server
\\DataServer\Log : Folder where the data server log is saved (Folder must be made and rady)

2.	Cooperate with GameServer, and works as user data save and load.
3.	Make shortcut of DataServer.exe with extension 
4.	Extension is set for the DataServer port number, and window location
5.	예)
a.	1st  DataServer.exe :  set as “C:\MuOnline\DataServer\Dataserver.exe 55960 1”
b.	2nd DataServer.exe : set as “C:\MuOnline\DataServer\Dataserver.exe 55962 2”  
 
6.	\Data Folder
a.	File structure
commonserver.cfg	It has game server option. If it is modified, it affects the game (Primary subjects must be modified while server setting)
dataserver.ini
dataserver.ini.dat	It contains options for DB Server.
eventitembagX.txt	Item list which is used on (Golden Budge Dragon)
gate.txt	Movement information while using move
item(Vie).txt	Item information
message_tai.wtf	Server Text
Monster.txt	Monster Information
MonsterSetBase.txt	Monster location information
ServerInfo.data	Gameserver execution information
ShopX.txt	Item list of 0 to N, which are sold in the shop
Skil.txt	Magic and Skill information
TerrainX.att	The property of Map 1 to N
badsyntax.txt	File to check unwanted words to be used in character DB server.
※ . there are more data files are available

b.	Use them in DataServer, ExDB, GameServer
c.	GameServer is shared as M drive (this Data folder must be shared, after the setup of DataServer on the host.)

 
iii.	Installation of ExDB
1.	File structure
\\ExDB\Exdb.exe : ExDB execution file
\\ExDB\exdb.ini : ExDB setting file
\\ExDB\exdb.ini.dat : ExDB setting file (encrypted)
\\ExDB\LogProc.dll : Required DLL
\\ExDB\LOG : ExDB Folder where the log is saved (it must be made before using)

2.	Manage the guild and my friend required data
3.	Make shortcut of Ex.ex and extension added
4.	Extension has ChatServer Public IP
a.	GameServer brings IP of ChatServer from ExDB, then tells Client
5.	Example)
a.	 Set as “C:\MuOnline\ExDB\ExDB.exe xxx.xxx.xxx.xxx” 
 
5.	Installation of GameServer
A.	File Structure
\\GameServer\GameServer\GameServer.zip : Game server execution file (normal)
\\GameServer\GameServer\GameServer_CS.zip : Game server execution file (for Castle Siege)
\\GameServer\GameServer\WzAG.dll : required DLL
\\GameServer\GameServer\mumsg.dll : required DLL
\\GameServer\GameServer\ggsrvdll.dll : Game guard DLL (reserved)
\\GameServer\GameServer\ggauth.dll : Game guard DLL (reserved)
\\GameServer\GameServer\Log\ : Folder where the Gameserver log is saved (It must be made before using)
\\GameServer\Data\ServerInfo.dat : Game server unique code, PK server on/off is saved on the data file (Each server has own unique code -> Not like Data folder in DataServer, it is available on the upper folder of Data folder)

B.	Share the Data folder as M drive, from DataServer
C.	Check the information in \GameServer\Data, ServerInfo.dat
[GameServerInfo]
ServerName       = 1-1	// Each server has unique code just like ServerCode
ServerCode       = 0		// Code for Data\ ServerList.dat in CS. Each server has own unique code (IMPORTANT!!!)
NonPK	 = 0			// PK server seting (0:PK / 1:NonPK)
D.	Check the information in \\Data\lang\phi\commonlog.cfg
[ConnectServerInfo]
IP = 10.1.1.1		; ConnectServer address
PORT = 55557	 	; ConnectServer Port

E.	Unzip and setup Normal game server. GameServer.zip, and Castle Siege server, GameServer_CS.zip. To describe the Normal game server and Castle Siege server, Castle Siege server is available only 1 for each group. If there are 4 server group, (Server group which shares GameDB) Each server group has 1 C.S server, therefore it means 4 C.S server total. See the diagram. (White is normal game server, yellow is C.S server)
 
F.	Each server group must be set the MapServerInfo.dat in M drive. This file is the map structure table, and is owned by each server group. If this file has wrong setting, then Castle Siege will be played. To set this file, refer the file below.
\\Document\CastleSiege_Setting.doc
\\Document\MapServerData_SettingExam.doc

G.	Make shortcut of GameServer.exe
i.	Extension setup : JoinServerIP JoinServerPort DataServerIP DataServerPort GameServerPort
ii.	Example)
1.	 “10.1.224.217 55970 10.1.1.23  55960 55901

 
6.	Installation of ChatServer
A.	File structure
\\ChatServer\ChatServer.exe : Chat server execution file
\\ChatServer\LogProc.dll : required DLL
\\ChatServer\WZSock.dll : required DLL
\\ChatServer\Log\ : Folder where the chat server log is saved (it must be made before using)

B.	Make shortcut of ChatServer.exe
i.	Extension setting : set as ExDB private IP
ii.	example)
1.	“C:\MuOnline\ChatServer\ ChatServer.exe xxx.xxx.xxx.xxx”
 
7.	Installation of WzFsGate
A.	File Structure
\\WzFsGate\WzFsGate.exe : 
\\WzFsGate\Log\ : Folder where WzFsGate server log is saved (It must be made before using)

B.	Data management for GameServer
C.	O/S, in Windows Server subfolder, open ‘C:\WINDOWS\system32\drivers\etc\hosts’, and then put below subjects 
218.38.44.100	gsauth.muonline.co.kr
D.	Above IP is the game authentic server in Korea, and 55909 port is used. Therefore please check using be telnet on  WzFsGate server host, and check as the method below.
telnet gsauth.muonline.co.kr 55909
E.	Execute WzFsGate.exe to check if it receives data properly.
 
8.	Installation of Connect Server
A.	File Structure
\\ConnectServer\CS.exe : Connect Server execution file
\\ConnectServer\DATA\ServerInfo.dat : Connect server information file
\\ConnectServer\DATA\ ServerList.dat : Game server list information file

B.	Check the \CS\Data, ServerList.dat 
1.	“Servercode, Servername, Serveraddress, Serverport check(“SHOW”/”HIDE”)”
2.	example)
a.	“0 "GameServer1-1" "10.1.100.4" 55901 "SHOW"”
3.	Severcode is the unique data in each game server, defined in ServerInfo.dat
4.	If serverIP which is sent as UDP data, to Connect server, and Servercode is not same, then game server is not added on the connect server list.

C.	Check \ConnectServer\Data, ServerInfo.dat 
[FtpServerInfo]
Address = xxx.xxx.xxx.xxx	;Client Auth Patch FTP address
Port    = 21			; FTP Port
ID      = MuUpdate		; FTP account
PASS	= MuUpdate

[GameServerInfo]
ClientVersion = 00.98.03		; Client Normal server version
ClientVersion_TEST = 00.98.03 	; Client Test server version
VersionFileName = version.wvd	; version information file

 
9.	Installation of Ranking Server
A.	File Structure
\\RankingServer\MU_RANKING_DB_SERVER.exe : Ranking server execution file
\\RankingServer\svconfig.ini : Ranking server setting file
		
B.	Ranking server is available only 1 in total game server system(except China) It saves the ranking from DevilSquare, BloodCastle.

C.	Creation of Ranking DB
i.	DB for event ranking information management.
ii.	Choose master DB
iii.	Using Query Analyzer, find the folder \\DbScript\Ranking , then open and execute  Ranking_CreateDB.sql, Ranking.sql 
1.	File Structure
\\DbScript\Ranking\Default_ODBC.txt
\\DbScript\Ranking\Ranking.sql
\\DbScript\Ranking\Ranking_CreateDB.sql

iv.	Check the availability of Ranking DB and Table and SP 
v.	Table and SP which are created in DB, please refer to the document.

D.	ODBC setup
Refer to \\DbScript\Ranking\Default_ODBC.txt
		
E.	Check the information in \RankingServer\Data, svconfig.ini

[odbc_setting]
dbname=Ranking
odbc_dsn=RANKING_DATA
odbc_uid=MuOnlineAdmin
odbc_pass=wkfwkRnfRnf
odbc_con_count=40


[pim_setting]
queue_no=4
workerthread_no=10

 
10.	Installation of Event Server
A.	File Structure
\\EventServer\WZ_MU2003_EVENT_SERVER.exe : event server execution file
\\EventServer\DATA\svconfig.ini : event server setting file
\\EventServer\DATA\MU2003_MUTTO_NUMBER.TXT : event server data file
		
B.	Event server is available only one in total game server system (except China). This server has the function for saving user data while event, and restoring prize information.

C.	MU2003_EVENT_DATA DB setup
i.	DB for event information management
ii.	Choose master DB
iii.	On Query Analyzer, find the folder \\DbScript\Event, MU2003_EVENT_DATA_CreateDB.sql, and then open and execute MU2003_EVENT_DATA.sql
1.	File Structure
\\DbScript\Event\Default_ODBC.txt
\\DbScript\Event\MU2003_EVENT_DATA.sql
\\DbScript\Event\MU2003_EVENT_DATA_CreateDB.sql

iv.	Check the availability of MU2003_EVENT_DATA DB, Table and SP
v.	Refer to the document about DB if you want to know about Table and SP

D.	ODBC setting
Refer to \\DbScript\Event\Default_ODBC.txt
		
E.	Check the folder \EventServer\DATA, and then svconfig.ini

[pim_setting]
queue_no=4
workerthread_no=4

[odbc_connection]
mu2003_dbname = MU2003_EVENT_DATA
mu2003_dsn = MU2003_EVENT_DB
mu2003_uid = MuOnlineAdmin
mu2003_pass = wkfwkRnfRnf

