Instructions for Building the Codalite Solutions Website (AI Development Guide)
Project Goal: Develop the Codalite Solutions website as outlined in the "Product Requirement Document: Codalite Solutions Website" Canvas. The project will leverage Python (Django), HTMX, Alpine.js, and Tailwind CSS. Adherence to the phased development approach (Section 10 of the PRD), technical requirements (Section 8), and branding guidelines (Section 4) is paramount.

Phase 0: Foundational Setup & Project Structure
Objective: Establish the core Django project, configure essential settings, and create the base templating system.

Django Project Initialization:

Create a new Django project named codalite_project.

Initialize the following core Django applications:

core: For general utilities, base templates, and static pages (e.g., Homepage, About Us, Contact Us).

services: To manage IT consultancy and software development content.

training: To manage course catalog, online learning platform, and offline class information.

accounts: For user authentication and profile management.

Configure settings.py:

Set up DATABASES for PostgreSQL (using environment variables for credentials).

Configure STATIC_URL and MEDIA_URL for development to serve locally.

Implement a conditional configuration to use Cloudflare R2 for static and media files in production.

Add all created apps to INSTALLED_APPS.

Implement basic security settings: SECRET_KEY, ALLOWED_HOSTS, CSRF_COOKIE_SECURE, SESSION_COOKIE_SECURE, SECURE_BROWSER_XSS_FILTER, SECURE_CONTENT_TYPE_NOSNIFF.

Integrate Tailwind CSS setup (e.g., django-tailwind or manual PostCSS/Webpack setup if preferred, but prioritize CDN for initial setup if simpler).

Configure Django's authentication system to use custom user models if needed for future LMS extensions (e.g., AbstractUser).

Base Template (base.html):

Create a robust, responsive base.html template that serves as the foundation for all pages.

Include the Tailwind CSS CDN, Alpine.js CDN, and HTMX CDN in the <head> or just before </body> as appropriate for performance.

Implement a responsive header/navigation bar using Tailwind CSS, incorporating the Codalite logo (placeholder for received_1708532489751492~2.jpeg) and primary navigation links (Home, Services, Training, About Us, Contact Us). Use the specified color palette (Primary Purple: #9933FF, Accent Cyan/Aqua: #00FFFF, Dark Neutral: #1A1A1A, Light Neutral: #F5F5F5).

Include a {% block content %} area for page-specific content.

Add a responsive footer with copyright information, quick links, and social media icons.

Ensure proper meta viewport tag for responsiveness.

Phase 1: Minimum Viable Product (MVP) - Core Marketing Site
Objective: Launch a foundational website to establish online presence and capture basic leads.

Homepage (Section 5.1):

Django: Create a view (core.views.homepage) and URL (path('', views.homepage, name='home')).

Template (home.html):

Hero Section: Design a visually appealing hero section with a catchy headline, clear value proposition, and a prominent "Request a Consultation" button styled with the primary purple. Ensure it's responsive and uses the Inter font.

Services Overview: Include brief, visually distinct sections for "IT Consultancy," "Software Development," and "Training," each with a short description and a link to their respective overview pages.

Key Differentiators: A section highlighting 3-4 unique selling points of Codalite Solutions.

Client Testimonials/Logos: Placeholder section for future testimonials or client logos.

Call-to-Action: A final call-to-action leading to the Contact Us page.

Contact Us Page (Section 5.5 - Basic):

Django: Create a ContactForm in core.forms.py, a view (core.views.contact_us) to handle GET and POST requests, and a URL (path('contact/', views.contact_us, name='contact')).

Template (contact.html):

Design a clean contact form (Name, Email, Subject, Message).

Implement form submission using HTMX (hx-post, hx-target, hx-swap). Upon successful submission, display a success message on the page without a full reload. On error, display validation errors.

Include placeholder for phone number, email, and social media links.

Basic Services Overview Pages (Section 5.2):

Django: Create services.views.it_consultancy and services.views.software_development views with corresponding URLs.

Templates: Create it_consultancy.html and software_development.html. Each should have a clear title, a brief descriptive paragraph of the service, and a prominent "Request a Quote" or "Start Your Project" button linking to the Contact Us page.

Basic Training Overview (Section 5.3 - Course Catalog List):

Django: Create a training.views.course_catalog view and URL.

Model (training.models.Course): Define a simple Course model with fields like title, slug, short_description, difficulty, format (choices: 'online', 'offline'). Register this model with the Django admin.

Template (course_catalog.html): Display a list of courses (initially, a few dummy courses can be created via the admin). Each course item should show its title, short description, and a link to a future detailed course page.

About Us Page (Section 5.4 - Basic):

Django: Create a core.views.about_us view and URL.

Template (about.html): Include placeholder sections for "Our Story" and "Team Page."

Blog (Section 6.1 - Basic Functionality):

Django: Create a blog app. Define a Post model with title, slug, content, published_date, author. Register with admin. Create blog.views.post_list and blog.views.post_detail views and URLs.

Templates: post_list.html to display a list of blog post titles and summaries. post_detail.html for individual post content.

Phase 2: Enhanced Marketing & Lead Generation
Objective: Improve lead capture and showcase expertise.

Detailed Service Pages (Section 5.2) with Case Studies (Section 6.2):

Django: Enhance services app. Create a CaseStudy model (title, description, client, technologies_used, results, link_to_project - if external). Link CaseStudy to Service models.

Templates: Update it_consultancy.html and software_development.html to include a section displaying relevant case studies. Create case_study_detail.html for individual case study pages.

Interactive "Problem Solver" / Needs Assessment Tool (Section 6.3):

Django: Create a series of views or a single view with conditional logic to handle a multi-step questionnaire. Store user responses temporarily (e.g., in session or a temporary model).

HTMX/Alpine.js: Implement the questionnaire using HTMX for partial updates between steps. Use Alpine.js for simple client-side UI enhancements (e.g., progress bar, input validation hints).

Lead Capture: Upon completion, capture the user's input and generate a lead for the sales team (e.g., save to a Lead model, send an email notification via Celery).

Resource Library (Section 6.5):

Django: Create a Resource model (title, description, file_upload, requires_email).

Template: Display downloadable resources. Implement an email capture form using HTMX. After email submission, provide a link to download the resource.

Newsletter Subscription (Section 6.7):

Django: Create a simple NewsletterSubscriber model (email, subscribed_date).

Template: Add a prominent newsletter signup form (email input, subscribe button) in the footer or a dedicated section. Use HTMX for submission.

Live Chat / Chatbot Integration (Section 6.4):

Frontend: Integrate a third-party live chat widget (e.g., Tawk.to, Crisp, or a custom solution if simple). This will primarily be a frontend integration.

Phase 3: Online Learning Platform (LMS)
Objective: Enable online course delivery and management.

User Authentication & Profiles (Section 8.3):

Django: Implement robust user registration, login, logout, password reset, and profile management using Django's built-in authentication system. Consider extending AbstractUser for future custom fields.

Templates: Design user-friendly login, registration, and profile pages.

Full Course Detail Pages (Section 5.3):

Django: Enhance the Course model with fields for full_description, learning_objectives, curriculum_outline (JSONField or rich text field), price, instructor (ForeignKey to User/Instructor model). Create an InstructorProfile model.

Templates: Design comprehensive course detail pages. Include "Enroll Now" button.

Payment Gateway Integration (Section 7.2):

Django: Integrate with Stripe or PayPal for secure payment processing. Implement necessary views and webhook handlers for successful transactions.

Models: Create Enrollment model (user, course, enrollment_date, status, payment_id).

Student Dashboard (Section 5.3):

Django: Create a training.views.student_dashboard view (authenticated access only).

Template: A personalized dashboard showing enrolled courses, progress, and quick links to course materials.

Course Content Delivery (Section 5.3):

Django: Create models for Module, Lesson, ContentItem (e.g., Video, TextContent, FileDownload). Link these to Course. Use Django's file/image fields for content uploads.

Templates: Design interfaces for viewing course content.

Interactive Quizzes (Section 5.3):

Django: Create Quiz, Question, Option, UserAnswer models. Implement logic for quiz presentation and scoring.

HTMX/Alpine.js: Use HTMX to load quiz questions dynamically. Alpine.js for client-side quiz logic (e.g., showing immediate feedback, tracking selected answers before submission).

Progress Tracking (Section 5.3):

Django: Implement logic to track student progress (e.g., UserCourseProgress model tracking completed lessons/modules, quiz scores).

Templates: Display progress bars or completion statuses on the dashboard and course pages.

Certificate Generation (Section 5.3):

Django: Implement a mechanism to generate certificates (e.g., using a library like Pillow or ReportLab to create PDFs) upon course completion. Store certificate details and provide a download link. This should be an asynchronous task using Celery.

Discussion Forums (Section 5.3):

Django: Create Forum, Topic, Post models. Implement basic forum functionality (creating topics, replying to posts).

Templates: Integrate discussion areas within course pages.

Phase 4: Continuous Improvement & Advanced Features
Objective: Refine existing features and introduce advanced functionalities.

Advanced LMS Features:

Assignments & Grading: Models for Assignment, Submission, Grade. Instructor interface for reviewing and grading.

Live Sessions: Integration with a video conferencing API (e.g., Zoom, Google Meet) for scheduling and joining live online classes (as previously noted, this is a later phase).

Personalized Content Recommendations:

Implement basic recommendation logic based on user's enrolled courses, viewed content, or quiz performance.

Career Opportunities / Job Board (Section 6.6):

Django: Create JobPosting model (title, description, requirements, application_link/form).

Templates: A dedicated careers page with job listings and an application form.

Client Portal (Future Consideration):

A secure, authenticated area for business clients to view project progress, share files, and communicate with their dedicated team.

General Implementation Guidelines (Throughout All Phases):
Adherence to PRD: Strictly follow all requirements in the provided Canvas, especially regarding:

Branding & Design (Section 4): Use the specified color palette, typography (Inter font), and ensure high-quality, professional imagery.

Technical Requirements (Section 8):

Performance: Optimize images, implement lazy loading, consider caching strategies (Django's caching framework with Redis).

Scalability: Design for statelessness where possible, consider Celery for background tasks.

Security: Implement all OWASP Top 10 mitigations, ensure proper authentication/authorization, input validation, CSRF/Clickjacking protection, and secure password handling.

Accessibility: WCAG 2.1 AA compliance (semantic HTML, keyboard navigation, alt text, color contrast).

SEO: Clean URLs, meta tags, structured data.

Responsiveness: Mobile-first design using Tailwind CSS utility classes.

Information Architecture (Section 9): Follow the defined sitemap and URL structure.

Code Quality:

Clean Code: Write readable, maintainable, and well-organized code.

Comments: Provide extensive comments for all functions, classes, complex logic, and template sections.

Error Handling: Implement robust error handling in both Django views and frontend JavaScript (Alpine.js). Provide user-friendly error messages.

Modularity: Keep Django apps and templates modular and reusable.

Testing Considerations:

While not explicitly asked to write tests, design the code to be testable.

Consider basic validation for all forms and data inputs.

