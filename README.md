# StartTech Application

A full-stack task management application built with React (frontend) and Go (backend), deployed on AWS with a complete CI/CD pipeline.

## Live URLs

- Frontend: http://muchtodo-frontend-dev.s3-website-us-east-1.amazonaws.com
- Backend API: http://muchtodo-alb-final-425877782.us-east-1.elb.amazonaws.com
- CloudFront: https://dzbg5w9pb03gl.cloudfront.net


## Architecture

- Frontend: React (TypeScript) hosted on AWS S3, served globally via CloudFront CDN
- Backend: Golang API containerized with Docker, deployed on EC2 behind an Application Load Balancer
- Database: MongoDB Atlas for data persistence
- Cache: AWS ElastiCache Redis for session and data caching
- Container Registry: AWS ECR for storing Docker images
- Infrastructure: All provisioned with Terraform (see starttech-infra repo)


## CI/CD Pipelines

### Frontend Pipeline
Triggers automatically on push to main when frontend files change:
1. Installs Node.js dependencies
2. Builds production React bundle
3. Runs security scan
4. Syncs build files to S3
5. Invalidates CloudFront cache

### Backend Pipeline
Triggers automatically on push to main when backend files change:
1. Runs Go unit tests
2. Builds Docker image
3. Pushes image to AWS ECR
4. SSHs into EC2 and deploys new container

## Tech Stack

sorry change this build cause it looks weird on github 

```markdown
| Layer | Technology |
|-------|-----------|
| Frontend | React, TypeScript, Tailwind CSS |
| Backend | Golang |
| Database | MongoDB Atlas |
| Cache | AWS ElastiCache Redis |
| Container | Docker |
| Registry | AWS ECR |
| CDN | AWS CloudFront |
| Storage | AWS S3 |
| Load Balancer | AWS ALB |
| CI/CD | GitHub Actions |
| Infrastructure | Terraform |
```

## Local Development

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Backend
```bash
cd backend/MuchToDo
cp .env.example .env
go run main.go
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| MONGO_URI | MongoDB Atlas connection string |
| REDIS_ADDR | ElastiCache Redis endpoint |
| JWT_SECRET_KEY | Secret key for JWT tokens |
| SERVER_PORT | Port to run the server on |

## Repository Structure

```
starttech-application/
├── .github/
│   └── workflows/
│       ├── frontend-ci-cd.yml
│       └── backend-ci-cd.yml
├── frontend/
├── backend/
│   └── MuchToDo/
└── README.md
```