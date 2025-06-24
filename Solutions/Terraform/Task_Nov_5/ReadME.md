# Open IAM in AWS to create user 
#I have created (Admin-Cli) as a user 
#Assign policy  (AdministratorAccess)
#create Acces key from Security credentials
#choose Command Line Interface (CLI) as a use case 
#Access key : ****************
#Secret key : ************************
#I can put them in the text.tf provider or use the AWS extention 

#ex.tf

provider "aws" {
  region = "us-east-1"  # Update to your preferred region if necessary
  access_key = "AKIAZKB25LZEVCAHXMBR"
  secret_key = "bCoTa1Edjmx2tsxSb+akoYrf/1MaF2XN5Vo7fqxg"

}

# Data source to get the default VPC
data "aws_vpc" "default" {
  default = true
}

# Public Subnet
resource "aws_subnet" "public_subnet" {
  vpc_id                  = data.aws_vpc.default.id   
  cidr_block              = "172.31.1.0/24"          
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true
}

# Private Subnet
resource "aws_subnet" "private_subnet" {
  vpc_id            = data.aws_vpc.default.id        
  cidr_block        = "172.31.2.0/24"                
  availability_zone = "us-east-1b"
}


# Create a Security Group to Allow HTTP (80) and SSH (22) Traffic
resource "aws_security_group" "web_sg" {
  vpc_id = data.aws_vpc.default.id
  name   = "web-security-group"

  # Allow HTTP traffic on port 80
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Allow SSH traffic on port 22
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Allow all outbound traffic
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}



# Create an EC2 Instance
resource "aws_instance" "web_server" {
  ami           = "ami-06b21ccaeff8cd686"  # Amazon Linux AMI in us-east-1 
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.public_subnet.id
  vpc_security_group_ids = [aws_security_group.web_sg.id]

  tags = {
    Name = "web-server" 
  }
}
