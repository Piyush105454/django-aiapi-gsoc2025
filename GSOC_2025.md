GSoC 2025 Proposal: Django AI-Powered REST API Framework for Rapid Prototyping

1. Motivation

With the rapid rise of AI applications, many developers face the challenge of quickly integrating machine learning models into web applications—particularly with Django. Although Django REST Framework (DRF) simplifies API building, it still requires significant boilerplate and lacks first-class support for integrating AI/ML models seamlessly.
This proposal introduces a plug-and-play Django extension to enable AI model integration, dynamic REST endpoint generation, and schema auto-documentation, reducing the setup time for AI developers.
Inspired by tools like FastAPI and Flask-RESTPlus, the goal is to bring that ease to Django while leveraging its maturity, admin interface, and ORM.

2. Proposal

2.1 AI API Schema Generator

A declarative syntax to connect AI/ML models (trained in TensorFlow, PyTorch, or scikit-learn) and automatically expose them as REST endpoints.
from django_aiapi import AIModelView

class SentimentAnalysisView(AIModelView):
    model_path = "models/sentiment.pkl"
    input_schema = {"text": "string"}
    output_schema = {"sentiment": "string", "confidence": "float"}

This will:
Load the model
Validate the input using pydantic or DRF serializers
Serve prediction output at /predict/sentiment-analysis/


2.2 Model Registry & Dynamic Routing

A registry to track all registered AI models and auto-generate routes.
AIRegistry.register(SentimentAnalysisView)
Auto-generates /predict/ endpoints for each registered view
Adds metadata to Swagger/OpenAPI docs


2.3 REST API Builder for CRUD

Introduce a lightweight decorator and base class for generating CRUD APIs with minimal code.

@autocrud
class Book(models.Model):
    title = models.CharField(max_length=255)
    author = models.CharField(max_length=255)

This auto-generates:
/api/books/ (GET, POST)
/api/books/<id>/ (GET, PUT, DELETE)
Serializer + ViewSet + URLConf without writing extra code


2.4 Swagger + AutoDocs Integration

All APIs generated are auto-documented using Swagger and ReDoc with support for:
Input/output schema visualization
Model metadata
Test playground


2.5 Backend Performance Boost with C++/ONNX

Optional integration to load ONNX models and accelerate backend AI inference using:
PyTorch/TensorFlow → ONNX export
C++ inference engine (via bindings)


3. Scope of Work

Phase 1 (Community Bonding & Research)
Study Django's class-based views, DRF internals
Explore FastAPI-style model serving
Finalize architecture and folder structure


Phase 2 (175 hrs)

Build AIModelView and AIRegistry
Develop model loader for .pkl, .pt, .onnx
Test with dummy sentiment model


Phase 3 (175 hrs)


Develop @autocrud decorator and admin integration
Implement full Swagger/OpenAPI doc generation
Package and release as django-aiapi


4. Deliverables


django-aiapi open-source package
Docs + Tutorials (e.g. deploy an AI model in 5 minutes with Django)
Working example apps:
Sentiment Analyzer
Image Classifier
CRUD APIs with @autocrud
Performance benchmarks (DRF vs AIAPI)


5. Benefits to Django Community


Encourages AI/ML developers to use Django
Reduces friction for data scientists to serve models
Makes Django competitive with FastAPI for AI use-cases
Easier prototyping for startups & hackathons


6. About Me
Hi, I'm Piyush Tamoli, a first-year ALML student passionate about AI and backend development. I actively work with Django, REST APIs, and AI models in Python. I've built projects like SwapEat (Django + WebSocket food sharing + api food detection + map), and an AI tools aggregator.
Through GSoC, I want to contribute to Django by making AI deployment faster, simpler, and more accessible for everyone.

[https://github.com/Piyush105454]
[https://www.linkedin.com/in/piyush-tamoli-751b2125a?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app]
Swapeat : [https://github.com/Piyush105454/swap-eat]

