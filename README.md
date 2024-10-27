## Prerequisites

### Configure AWS Credentials
- Copy `AWS access_key`, `secret_key`, and `session_token` from **AWS Details**
- Paste into `~/.aws/credentials` file
- Download PEM file under SSH key for EC2 terminal access

This step is important for the code to run, NOTE : the access credentials are temporary and change after every session reset or after 3 hours.

## Creating EC2 Instances

### Launch Two EC2 Instances
1. Go to **EC2 Dashboard** → **Launch Instance**
2. Select **Amazon Linux 2 AMI (HVM)** with `t2.micro` type
3. Name your instances (e.g., EC2-A and EC2-B)
4. Choose `create new key pair` as Key-Pair value and download it for SSH.
5. Under **Network Settings**, create security group with:
   - SSH traffic
   - HTTP/HTTPS traffic from internet
   - Change "Anywhere" to "My IP"
6. Keep default **Configure Storage** and **Advanced Details**

![Alt text](Screenshot%202024-10-26%20011232.png)

## Logging into the EC2 instances on your local machine

```bash
ssh -i "path-to-key.pem" ec2-user@public-ip
```

## Working with Java Programs

### Installing Java and Maven

Install Java:
```bash
sudo yum install java-1.8.0-openjdk
```

Install Maven:
```bash
sudo yum install maven
```

### Create Project Structure with Maven
Generate basic structure using:
```bash
mvn archetype:generate \
    -DgroupId=com.example \
    -DartifactId=my-java-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Here put your desired folder name instead of my-java-project

### Converting to JAR and Running
Build project and create JAR:
```bash
mvn clean package
```

Run the Java program:
```bash
java -jar target/my-java-project-1.0-SNAPSHOT.jar
```

### Execute the Programs
Run object detection(EC2-A):
```bash
java -jar AWSObjectDetection.jar
```

This is the output we get after running the code.
![Alt text](Screenshot%202024-10-26%20010910.png)

We can also see in the AWS console that a queue has been created and we can retrieve the results using the "Polling for messages" option
![Alt Text](Screenshot%202024-10-26%20010926.png)

![Alt Text](Screenshot%202024-10-26%20010939.png)


Run text detection with output file(EC2-B):
```bash
java -jar AWSTextRekognition.jar > output.txt
```

On running the Text recognition we can see this output:
![Alt Text](Screenshot%202024-10-26%20011232.png)
