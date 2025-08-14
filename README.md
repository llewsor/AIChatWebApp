# AI Chat Web App

A modern AI-powered chat application built with ASP.NET Core 9.0 and Blazor Server that enables intelligent conversations with your custom documents. This application uses GitHub Models API with OpenAI GPT-4o-mini for chat and text-embedding-3-small for semantic search capabilities.

## ✨ Features

- **💬 Interactive Chat Interface**: Clean, responsive chat UI built with Blazor Server components
- **📄 Document Integration**: Upload and chat with PDF documents using semantic search
- **🔍 Vector Search**: Advanced semantic search powered by SQLite vector database
- **🤖 AI Models**: Powered by GitHub Models API (GPT-4o-mini & text-embedding-3-small)
- **⚡ Real-time Updates**: Server-side rendering with SignalR for responsive interactions
- **🎨 Modern UI**: Styled with Tailwind CSS for a contemporary look and feel
- **🔐 Secure**: Uses user secrets for API key management

## 🏗️ Architecture

- **Frontend**: Blazor Server Components with Tailwind CSS
- **Backend**: ASP.NET Core 9.0 with dependency injection
- **AI Integration**: Microsoft.Extensions.AI with OpenAI connector
- **Vector Database**: SQLite with vector extensions for semantic search
- **Document Processing**: PDF parsing and chunking for optimal AI retrieval

## 📋 Prerequisites

- [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- [GitHub Personal Access Token](https://github.com/settings/personal-access-tokens/fine-grained) with `models:read` permission
- Visual Studio 2022, VS Code, or JetBrains Rider (optional)

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/llewsor/AIChatWebApp.git
cd AIChatWebApp
```

### 2. Configure GitHub Models API

Create a GitHub Personal Access Token with `models:read` permission:

1. Go to [GitHub Settings → Personal Access Tokens → Fine-grained tokens](https://github.com/settings/personal-access-tokens/fine-grained)
2. Click "Generate new token"
3. Name: "AI Chat WebApp"
4. Expiration: Set as needed (90 days recommended)
5. **Repository access**: Public Repositories (or specific repos)
6. **Account permissions** → **Model capabilities** → **Read**
7. Generate and copy the token

### 3. Set Up User Secrets

```bash
cd AIChatWebApp
dotnet user-secrets set GitHubModels:Token "your_github_token_here"
```

### 4. Restore Dependencies

```bash
dotnet restore
```

### 5. Run the Application

```bash
dotnet run
```

Navigate to `https://localhost:7026` or `http://localhost:5123` to access the application.

## 📚 Usage

### Adding Documents

1. Place PDF files in the `wwwroot/Data` directory
2. The application automatically processes these files on startup
3. Documents are chunked and embedded for semantic search

### Chatting with Documents

1. Open the chat interface
2. Ask questions about your documents
3. The AI will search relevant content and provide contextual answers
4. Citations show which documents were used for responses

### Sample Documents

The application includes example PDF files:

- `Example_Emergency_Survival_Kit.pdf`
- `Example_GPS_Watch.pdf`

## 🔧 Configuration

### Application Settings

Configure in `appsettings.json` or `appsettings.Development.json`:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

### User Secrets

Store sensitive configuration using .NET User Secrets:

```bash
# Set GitHub Models API token
dotnet user-secrets set GitHubModels:Token "your_token"

# List configured secrets
dotnet user-secrets list
```

## 🏃‍♂️ Development

### Project Structure

```
AIChatWebApp/
├── Components/
│   ├── Layout/           # Shared layout components
│   └── Pages/
│       └── Chat/         # Chat-related Blazor components
├── Services/
│   ├── Ingestion/        # Document processing services
│   ├── SemanticSearch.cs # Vector search implementation
│   └── Models/           # Data models
├── wwwroot/
│   ├── Data/             # PDF documents for ingestion
│   ├── lib/              # Client-side libraries
│   └── app.css           # Application styles
└── Program.cs            # Application startup
```

### Key Components

- **DataIngestor**: Processes and chunks PDF documents
- **SemanticSearch**: Performs vector similarity search
- **Chat Components**: Interactive chat UI with citations
- **SQLite Vector Store**: Manages embeddings and metadata

### Adding Custom Document Sources

Implement `IIngestionSource` to support additional document types:

```csharp
public class CustomDocumentSource : IIngestionSource
{
    public string SourceId => "custom-source";

    // Implement required methods...
}
```

## 🔨 Building for Production

### Build the Application

```bash
dotnet build --configuration Release
```

### Publish the Application

```bash
dotnet publish --configuration Release --output ./publish
```

### Environment Variables

For production deployment, consider using environment variables instead of user secrets:

```bash
export GitHubModels__Token="your_token"
```

## 🧪 API Endpoints

The application primarily uses Blazor Server components, but here are the key internal services:

- **Chat Service**: Handles AI chat interactions
- **Semantic Search**: Vector similarity search
- **Document Ingestion**: PDF processing pipeline

## 🛠️ Dependencies

### Core Packages

- `Microsoft.Extensions.AI.OpenAI` - AI integration
- `Microsoft.SemanticKernel.Core` - AI orchestration
- `Microsoft.SemanticKernel.Connectors.SqliteVec` - Vector database
- `PdfPig` - PDF document processing

### Client Libraries

- Tailwind CSS - Styling framework
- PDF.js - PDF viewing capabilities
- DOMPurify - HTML sanitization
- Marked - Markdown parsing

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Troubleshooting

### Common Issues

**HTTP 401 Unauthorized Error**

- Ensure your GitHub token has `models:read` permission
- Verify the token is correctly set in user secrets
- Check token expiration date

**Document Not Found**

- Ensure PDF files are in `wwwroot/Data` directory
- Check application logs for ingestion errors
- Verify file permissions

**Build Errors**

- Ensure .NET 9.0 SDK is installed
- Run `dotnet restore` to restore packages
- Check for any missing dependencies

### Getting Help

- Check the [GitHub Issues](https://github.com/llewsor/AIChatWebApp/issues) page
- Review application logs for detailed error messages
- Ensure all prerequisites are properly installed

## 🔗 Related Resources

- [GitHub Models Documentation](https://docs.github.com/github-models)
- [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core)
- [Blazor Server Documentation](https://docs.microsoft.com/aspnet/core/blazor)
- [Microsoft.Extensions.AI](https://devblogs.microsoft.com/dotnet/introducing-microsoft-extensions-ai-preview/)

---

**Built with ❤️ using ASP.NET Core, Blazor, and GitHub Models**
