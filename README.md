### System Architecture & Security Features
1. AES-256 Encryption ( encryption.py ) :
   
   - Uses the AES-256 algorithm (via cryptography library) to encrypt sensitive user data before it ever touches the database.
   - Ensures that even if the database is stolen, the data remains unreadable without the encryption key.
2. Capability Code Mechanism ( db_manager.py ) :
   
   - Implemented a SQLCapability class.
   - Database operations are restricted: functions must acquire a valid "Capability Token" (Read/Write) to execute queries.
   - This acts as a strict gatekeeper, preventing unauthorized or accidental raw SQL execution.
3. Double-Layer Security Protocol :
   
   - Layer 1 (Application Level) : Input validation in app.py (e.g., regex checks on usernames) acts as a Web Application Firewall (WAF) to block malicious characters early.
   - Layer 2 (Database Level) : Uses Parameterized Queries within the secure interface to treat all inputs as data, not executable code, effectively neutralizing SQL injection attacks.
4. Cloud & Internet Accessibility :
   
   - Built with Flask , a lightweight framework that runs without heavy system requirements.
   - Configured to listen on 0.0.0.0 , making it accessible over the internet (when deployed to a cloud server or with port forwarding).
### Project Files
- app.py : The main web application with routes and Layer 1 security.
- db_manager.py : Handles database interactions securely using the Capability mechanism.
- encryption.py : AES-256 encryption logic.
- templates/ : HTML user interface (Login, Register, Dashboard).
### How to Run
1. Install Dependencies :
   ```
   pip install -r requirements.txt
   ```
2. Start the Server :
   ```
   python app.py
   ```
3. Access the System :
   - Open your browser to http://localhost:5000 (or your server's public IP).
   - Register a new user (Data will be encrypted).
   - Login to view the decrypted data in the secure dashboard.
