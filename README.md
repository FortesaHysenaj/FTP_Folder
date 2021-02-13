# FTP_Folder

Zhvillimi i aplikacionit që mundeson qe fajllat me ekstension .doc, .docx, .xls, .xlsx në një folder të caktuar të ngarkohen në një FTP server të caktuar duke përdorur modulin tkinter të Python.

## Teknologjia e perdorur

- Sistemi Operativ - Windows 10 Pro
- Gjuha Programuese - Python

## Pershkrimi

Në këtë detyrë, kemi shqyrtuar se si të përdorim FTP me Python për të dërguar dhe marrë skedarë nga një server përmes lidhjeve TCP/IP.

Për t'i bërë gjërat më të lehta dhe më abstrakte, ne kemi përdorur librarite tkinter dhe ftplib të Python te cilat ofrojn një sërë funksionesh që e bëjnë më të lehtë punën me FTP. Ne do të shohim zbatimin për ngarkimin dhe shkarkimin e skedarëve nga serveri, si dhe disa gjëra të tjera interesante që "tkinter" dhe "ftplib" na lejojnë të bëjmë.

## Çfarë është FTP?

FTP është një protokoll standard i rrjetit që përdoret për transferimin e skedarëve midis një klienti dhe serverit në një rrjet kompjuterik. FTP është një protokoll shumë i mirë-vendosur, i zhvilluar në vitet 1970 për të lejuar dy kompjuterë të transferojnë të dhëna në internet. Një kompjuter vepron si server për të ruajtur informacionin dhe tjetri vepron si klient për të dërguar ose kërkuar skedarë nga serveri. Protokolli FTP zakonisht përdor portin 21 si mjetin e tij kryesor të komunikimit. Një server FTP do të dëgjojë për lidhjet e klientit në portin 21.

## Puna me FTP dhe GUI ne Python

Moduli tkinter u përdor për të krijuar UI dhe moduli ftplib merret me navigimin/komandat e serverit.
Moduli ftplib është një librari e integruar që vjen tashmë e instaluar me Python, gjithçka që duhet të bëni është ta importoni në skenarin tuaj dhe mund të filloni të përdorni funksionet e tij. Për ta importuar atë, përdorni komandën e mëposhtme:

> `from ftplib import FTP` <br />

Pas kësaj, duhet të fillojmë një lidhje me serverin FTP me të cilin duam të hapim një lidhje komunikimi. Për ta bërë këtë, krijoni një shembull ftp:

> `ftp.connect(ip,port)` <br />

Funksioni connect() merr hostin dhe portin dhe fillon një sesion me serverin.

> `ftp.login(user,password)` <br />

Pastaj, login() merr një emër të përdoruesit dhe fjalëkalimin dhe përpiqet të vërtetojë sesionin tonë. Nëse kredencialet tona verifikohen, ne kemi hyrë në server dhe mund të fillojmë të dërgojmë më shumë komanda; nëse jo, një kundërshtim error_perm do të shfaqet.

Për të ngarkuar në të vërtetë një skedar, ne përdorim metodën storbinary():

> `filename = path.basename(filepath) with open(filepath, 'rb') as fh: ftp_cx.storbinary('STOR {}'.format(filename), fh)` <br />

Për të dërguar skedarin, ne duhet ta hapim atë në modalitetin e leximit binar, pastaj thirrim komanden storbinary(). Argumenti i parë "STOR" në storbinary është një komandë e vlefshme e FTP-se , zakonisht shenohet STOR pastaj emri i skedarit, pra "STOR filename" ku "filename" është ajo që dëshironi të quhen të dhënat e ngarkuara në server.
Argumenti i dytë është vetë objekti i skedarit. Kjo duhet të hapet në modalitetin binar pasi që ne po e dërgojmë atë si të dhëna binare. Kjo mund të duket e çuditshme pasi skedari CSV që po dërgojmë është në thelb një skedar teksti i thjeshtë, por dërgimi i tij si të dhëna binare garanton që serveri nuk do ta ndryshojë skedarin në asnjë mënyrë gjatë transportimit; kjo është pothuajse gjithmonë ajo që ne dëshirojmë kur transferojmë skedarë, pavarësisht nga natyra e të dhënave që shkëmbehen.
