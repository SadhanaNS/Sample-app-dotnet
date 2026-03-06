# 🐳 Sample .NET App — Docker Practice

A sample ASP.NET Core Razor Pages application used to **practise containerising a .NET application using Docker** — writing a Dockerfile, building an image, and running the app locally in a container.

---

## 🎯 Purpose

This repo was created to practise:
- Writing a **Dockerfile** for a .NET 6 web application
- Understanding **multi-stage Docker builds** for .NET apps
- Building a Docker image locally using `docker build`
- Running the containerised app using `docker run`
- Understanding `.dockerignore` to keep the build context clean

---

## 🏗️ App Overview

A simple ASP.NET Core **Razor Pages** web application scaffolded using the .NET CLI. The app itself is intentionally basic — the focus is entirely on the containerisation process, not the application logic.

| | |
|---|---|
| Framework | ASP.NET Core Razor Pages |
| .NET Version | .NET 6 |
| Language | C# |
| Purpose | Docker practice — not production code |

---

## 📁 Project Structure

```
Sample-app-dotnet/
├── Pages/                      # Razor Pages (HTML + C#)
├── wwwroot/                    # Static files — CSS, JS
├── Properties/                 # Launch settings
├── Program.cs                  # App entry point
├── appsettings.json            # App configuration
├── appsettings.Development.json
├── SampleWebApp.csproj         # Project file
├── SampleWebApp.sln            # Solution file
├── Dockerfile                  # ✅ Docker build instructions
├── .dockerignore               # ✅ Excludes bin/, obj/, .vs/
└── README.md
```

---

## 🐳 Dockerfile — What It Does

The Dockerfile uses a **multi-stage build** — a best practice for .NET apps:

```
Stage 1 — Build
  Uses SDK image → restores packages → builds the app

Stage 2 — Runtime
  Uses smaller runtime-only image → copies build output only
  Final image has no SDK, no source code — smaller and more secure
```

This keeps the final Docker image lean — only what's needed to run the app, not build it.

---

## 🚀 Running Locally with Docker

**Prerequisites:** Docker Desktop installed and running

```bash
# Clone the repo
git clone https://github.com/SadhanaNS/Sample-app-dotnet.git
cd Sample-app-dotnet

# Build the Docker image
docker build -t sample-dotnet-app .

# Run the container
docker run -p 8080:80 sample-dotnet-app

# Open in browser
http://localhost:8080
```

---

## 📚 Key Learnings

- How to write a Dockerfile for a .NET Razor Pages app
- Why multi-stage builds reduce final image size significantly
- What `.dockerignore` does and why `bin/`, `obj/`, `.vs/` should be excluded
- Difference between `dotnet build` and `dotnet publish` in Docker context
- How port mapping works with `-p 8080:80`
- How the SDK image differs from the runtime image

---

## 🔜 Next Steps Planned

- [ ] Set up Azure DevOps CI/CD pipeline to automate the Docker build
- [ ] Push image to Azure Container Registry (ACR)
- [ ] Deploy to Azure Kubernetes Service (AKS)
- [ ] Add Trivy image scanning to the pipeline

---

## 👩‍💻 Author

**Sadhana Singh** — Senior DevOps Engineer
[LinkedIn](https://linkedin.com/in/sadhana-singh226) · [GitHub](https://github.com/SadhanaNS)
Azure DevOps Expert (AZ-400) | Azure Administrator (AZ-104)
