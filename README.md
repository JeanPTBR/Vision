# <p align="center"> VISION - Emotion and Dog Breed Recognition.



## ⚙️ Version<a name="versao"></a>

Currently, **Version 1.0** of this project is available, released in October/2024.

## 📝 Project Description:

This project aims to receive user-submitted images and analyze the emotions detected within them. It will also verify if there are pets in the image and, if so, identify the breed, returning tips about the pet.

## 🎯 Project Specifications:

The project is divided into two main stages:

##### Part 1 - Emotion Detection:

- The project begins with the creation of an API using the Serverless framework, allowing the user to upload an image.
- The image is analyzed by Rekognition, which inspects the detected labels.
- After Rekognition's verification, the most reliable emotion detected in the image is returned.
- If there is more than one face, it analyzes and returns the results separately.

##### Part 2 - Emotions + Pet:

- The second part involves analyzing the image to detect emotions and verify if there is a pet in the image using Rekognition.
- If a pet is detected, the breed is identified.
- Upon identifying the breed, a text is generated via Bedrock with tips related to that breed.
- The following information is mandatory: Energy level and exercise needs, Temperament and Behavior, Care and Needs, Common Health Issues.
- After Rekognition's verification, the most reliable emotion detected in the image is returned.
- If there is more than one face, it analyzes and returns the results separately.
- Finally, the faces and tips for the pet are returned.

## ⚙️ Technologies Used:
<p align="center">
  <a href="https://go-skill-icons.vercel.app/">
    <img src="https://go-skill-icons.vercel.app/api/icons?i=vscode,python,aws,git,github,postman" />
  </a>
</p>



 - **VSCode**: IDE chosen to write, edit, and debug the project's code.
 - **Python**: Programming language used.
 - **Serverless/Lambda**: The project was developed using the Serverless framework. Lambda enables code execution without the need to manage servers.
 - **AWS Cloud**: AWS provides computing, storage, and image processing services, integrating them into a comprehensive solution that simplifies implementation with scalability and without the need to manage physical infrastructure.
 - **AWS Rekognition**: Used to analyze images and detect faces and pets in the submitted images.
 - **AWS Bedrock**: For AI implementation and generating pet breed-related text.
 - **Amazon S3**: Used to store the images to be analyzed by the application.
 - **AWS IAM (Identity and Access Management)**: Manages credentials and permissions for accessing AWS services, ensuring that application components interact securely.
 - **Git and Github**: For application version control.
 - **Postman**: To test the application's routes and functionality.

## 🛠 How to Open and Run This Project:

**1. Clone the repository**:

```
git clone https://github.com/JeanPTBR/Vision.git
```
**2. Open the cloned repository in an IDE of your choice; for this project, Visual Studio Code (VSCode) was used**:

**3. We recommend using a virtual environment to avoid version conflicts**:
```
python -m venv venv

.\venv\Scripts\activate

```
**4. To confirm successful access to the virtual environment, the prefix "venv" should appear in your project's terminal path, for example**:
```
(venv) PS C:\Users\user>
```
**5. In the terminal, install the Serverless framework with the command**:
```
npm install -g serverless
```
**6. After installing the project framework, configure your AWS credentials**:

##### Option 1 - Via AWS CLI (Recommended):

Install AWS CLI and configure your credentials using:

```
aws configure
```
You will be prompted to provide:

- AWS Access Key ID: Your access key.<br>
- AWS Secret Access Key: Your secret key.<br>
- Default region name: For example, us-east-1 (Choose the region you are using).<br>
- Default output format: Can be JSON.

**7. Install dependencies**:
```
npm install
pip install -r requirements.txt:
```

**8. Add Environment Variables**:

Create a `.env` file in the root directory with the Amazon Bedrock model ID as follows:
- `MODEL_ID`

**9. Deploy the application using the Serverless Framework**:

Now that everything is configured, deploy the application to AWS:

```
task deploy
```

##### This command will:

- Configure the API Gateway.<br>
- Set up other required AWS integrations.


**10. Check the Generated Endpoints**:

These endpoints are URLs for the Lambda functions. Use them to make API requests via a browser, Postman, or other tools:

```
  Deploying vision to stage dev (us-east-1)

Service deployed to stack vision-dev (85s)

Endpoints:
  GET - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/
  GET - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/v1
  GET - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/v2
  POST - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/v1/vision
  POST - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/v2/vision
Functions:
  health: vision-dev-health (25 MB)
  v1Description: vision-dev-v1Description (25 MB)
  v2Description: vision-dev-v2Description (25 MB)
  detectEmotion: vision-dev-detectEmotion (25 MB)
  detectPetAndEmotion: vision-dev-detectPetAndEmotion (25 MB)
```

**11. Test the API Locally**:

```
serverless invoke local --function v1Description
```

Using serverless-offline:
```
task run
```

Using serverless-offline and nodemon for automatic reload:
```
npx nodemon 
```

## Testing VISION:

1. **Upload the Image to the Bucket**:

    Select the image and upload it to the configured bucket.<br>

2. **Deploy the Application**:

    Deploy the application. Once validated, access it via POSTMAN.<br>

3. **Provide the Image Information**:

    Enter the bucket information and the name of the saved image.<br>

Example:
```json
{
  "bucket": "myphotosmo",
  "imageName": "pugs.jpg"
}
```

4. **Possible Returns After Image Analysis**:

**Null Response:**
```json
{
    "url_to_image": "https://myphotosmo.s3.amazonaws.com/2dogs.jpg",
    "created_image": "14-10-2024 09:36:19",
    "faces": [
        {
            "position": {
                "Height": null,
                "Left": null,
                "Top": null,
                "Width": null
            },
            "classified_emotion": null,
            "classified_emotion_confidence": null
        }
    ]
}
```

**Emotion Response:**
```json
{
    "url_to_image": "https://myphotosmo.s3.amazonaws.com/triste.jpg",
    "created_image": "14-10-2024 08:54:35",
    "faces": [
        {
            "position": {
                "Height": 0.4149770438671112,
                "Left": 0.4800688624382019,
                "Top": 0.24941901862621307,
                "Width": 0.1959000676870346
            },
            "classified_emotion": "SAD",
            "classified_emotion_confidence": 93.24629974365234
        }
    ]
}
```

**Pet Response:**
```json
{
    "url_to_image": "https://myphotosmo.s3.amazonaws.com/cachorro.jpg",
    "created_image": "14-10-2024 09:36:20",
    "pets": [
        {
            "labels": [
                {
                    "Confidence": 99.0054931640625,
                    "Name": "Animal"
                },
                {
                    "Confidence": 99.0054931640625,
                    "Name": "Dog"
                },
                {
                    "Confidence": 99.0054931640625,
                    "Name": "Pet"
                },
                {
                    "Confidence": 92.6964111328125,
                    "Name": "Hound"
                }
            ],
            "Tips": "1. Energy level: The breed is active and enjoys physical activities such as walks, runs, and games. It also likes mental activities like training and cognitive exercises. 2. Daily exercise needs: At least two daily walks of 30 minutes each, along with games and playtime, are recommended.
            3. Temperament: This breed is friendly with children and other animals but can be possessive with food. Early socialization is recommended.
            4. Special care needs: Regular baths, dental care, and nail maintenance are recommended. High-quality food and supplements for skin and coat health are necessary.
            5. Common health issues: This breed is prone to health problems such as obesity, eye conditions, and spinal issues. Regular vet checkups are advised."
        }
    ]
}
```

**Emotion + Pet Response:**
```json
{
    "url_to_image": "https://myphotosmo.s3.amazonaws.com/pessoa-pet2.jpg",
    "created_image": "14-10-2024 09:45:22",
    "faces": [
        {
            "position": {
                "Height": 0.23378419876098633,
                "Left": 0.3006735146045685,
                "Top": 0.15228010714054108,
                "Width": 0.1119609847664833
            },
            "classified_emotion": "HAPPY",
            "classified_emotion_confidence": 100.0
        }
    ],
    "pets": [
        {
            "labels": [
                {
                    "Confidence": 98.90979766845703,
                    "Name": "Animal"
                },
                {
                    "Confidence": 98.90979766845703,
                    "Name": "Dog"
                },
                {
                    "Confidence": 98.90979766845703,
                    "Name": "Pet"
                },
                {
                    "Confidence": 96.54975891113281,
                    "Name": "Golden Retriever"
                }
            ],
            "Tips": "1. Energy level: The breed is active and enjoys physical activities such as walks, runs, and games. It also likes mental activities like training and cognitive exercises. 2. Daily exercise needs: At least two daily walks of 30 minutes each, along with games and playtime, are recommended.
            3. Temperament: This breed is friendly with children and other animals but can be possessive with food. Early socialization is recommended.
            4. Special care needs: Regular baths, dental care, and nail maintenance are recommended. High-quality food and supplements for skin and coat health are necessary.
            5. Common health issues: This breed is prone to health problems such as obesity, eye conditions, and spinal issues. Regular vet checkups are advised."
        }
    ]
}
```

## 📂 Project Structure:

### Directory Structure:

The project is organized as follows:
```
Vision/                                             # Main directory of the Vision project
│
├── assets/                                         # Contains media files and visual resources of the project
│   ├── arquitetura-base.jpeg                       # Base system architecture image
│
├── development/                                    # Development directory with collections and scripts
│   ├── collections/                                # Contains Postman collections
│         └── vision.json                           # Vision-specific Postman collection
│   ├── taskpy/                                     # Automated scripts for development-related tasks
│
├── visao-computacional/                            # Computer vision module of the project
│     ├── api/                                      # Contains all API versions
│         ├── v1/                                   # API version 1
│             ├── handlers/                         # Handlers for managing API v1 requests
│         ├── v2/                                   # API version 2
│             ├── handlers/                         # Handlers for managing API v2 requests
│
│     ├── aplication/                               # Application logic for the computer vision module
│         ├── contrib/                              # Contains reused code throughout the project and custom exceptions
|         ├── core/                                 # Project settings and environment variables
│
│     ├── infrastructure/                           # System infrastructure-related files
│         ├── aws/                                  # Code for AWS services used
│         ├── schemas/                              # Input data schemas for the endpoints
│
├── .gitignore                                      # File to ignore files and directories in version control
├── .pre-commit-config.yaml                         # Pre-commit settings for automatic validations before commits
├── pyproject.toml                                  # Configuration file for dependencies and tools for the Python project
├── nodemon.json                                    # Nodemon configurations for server monitoring and automatic reload
├── package.json                                    # Node.js project dependencies and scripts
├── requirements.txt                                # Python dependencies required for the project
└── README.md                                       # Project instructions and documentation
```

## ⚖️ License:
This project is licensed under the [MIT License](LICENSE).

## 🌐 Team:
🧑 💻 This project was developed by:</br>
| [<img loading="lazy" src="https://avatars.githubusercontent.com/u/167718668?v=4" width=115><br><sub>Jean Carlos</sub>](https://github.com/JeanPTBR) | [<img loading="lazy" src="https://avatars.githubusercontent.com/u/97261564?v=4" width=115><br><sub>Gustavo Felipe</sub>](https://github.com/gusttavofelipe) | [<img loading="lazy" src="https://avatars.githubusercontent.com/u/25685390?v=4" width=115><br><sub>John Sousa</sub>](https://github.com/johnSousa23)  |  [<img loading="lazy" src="https://avatars.githubusercontent.com/u/173844663?v=4" width=115><br><sub>Moniza Oliveira</sub>](https://github.com/MONIZA-OLIVEIRA) |
| :---: | :---: | :---: | :---: |

