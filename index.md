# Manoa SRCH Curriculum Builder

## Table of contents

* [Overview](#overview)
* [Approach](#approach)
* [Developer Guide](#developer-guide)
* [Community Feedback](#community-feedback)
* [Use Cases](#use-cases)
* [Example enhancements](#example-enhancements)
* [Conclusion](#conclusion)
* [Team](#team)
* [Development History](#development-history)

## Aligning Objectives With Safety: SRCH Navigator Proposal

Modern computer science and engineering education continually changes and evolves, especially in areas such as socially responsible computing. However, while information on these topics continues to grow and develop, it is often fragmented, incomplete, or not clearly explained to the end user. Additionally, it becomes more and more difficult for instructors in this field to align their courses with these ever-changing subjects. This project proposes a system that bridges the gap between what instructors want students to learn and the content available to teach it.

*Problem:*

The Socially Responsible Computing Handbook (SRCH) is an evolving collection of content intended to support instructors. However, it is not designed as a traditional textbook for a single course. Instead, it is a resource where instructors are expected to select relevant material and apply it to their own courses, which proposes several challenges:

• Some content is too advanced or not aligned with a course’s learning objectives

• The SRCH is incomplete and continuously evolving

• There is no structured way to map course objectives to relevant material

• Instructors must manually curate content, leading to inconsistency and inefficiency

• There is no standardized workflow for sharing curated curriculum paths

Essentially, instructors are given a large resource, but without the tools to effectively organize and align it to their teaching goals.

*Solution:*

This project proposes a web application that allows instructors to:

• Define their own courses, categorized using Bloom’s Taxonomy

• Browse and search SRCH content

• Map course learning objectives to relevant SRCH material

• Contribute new material and share curated content with others

This system will serve as a tool to not only align curriculum with the SRCH subjects, but to allow instructors to help develop a platform that uses the SRCH as its basis. This application is designed specifically for instructors at the University of Hawai‘i at Mānoa, particularly those teaching ICS courses such as ICS 314, where integrating socially responsible computing topics into technical material is increasingly important.

## Approach
<!-- Expand the section below -->

SRCH Curriculum Builder has two user roles: instructors and administrators. Instructors are able to browsw and view SRCH curriculum currently available, and use the relevant topics to build out their course, and tie it into responsible computer practices. Administrators will be able to manage content posted by Instructors, and review posted content for relevance.

<!-- Expand the section above -->

### User Guide

To support the development of the platform, the application will use several key pages:

*Home Page:* A landing page introducing the platform and its purpose, along with quick access to login or course dashboards.

![](img/home.png)

*Login/Register:* An authentication system allowing instructors and editors to access their data and contributions.

![](img/updatedSignin.png)

![](img/login.png)

*User Profile Page:* Displays user information, courses created and contributed content.

![](img/profile.png)

*Course Management (CRUD):* Allows Admin to (CRUD) users and courses, manage course-specific learning objectives

![](img/AdminFunc.png)

*SRCH Content Browser:* Allows instructors to: view, filter and select existing SRCH topics

![](img/srchBrowser.png)

*SRCH Curriculum Gallery:* Allows instructors to: View existing curriculums and add their own curriculum path 

![](img/curriculum.png)

*SRCH Unmapped Objectives:* Allows instructors to: Create Objectives without mappings, view, like, comment and vote on unmapped objectives within a forum

![](img/unmapped.png)

## Developer Guide

This guide walks developers through downloading, installing, running, and modifying the SRCH Curriculum Builder system.

---

### 1. Clone the Repository

Clone the project locally:

```bash
git clone https://github.com/manoa-srch/srch-application-project.git
cd srch-application-project
```

---

### 2. Install Dependencies

Make sure you have Node.js (v18+) installed.

Then install dependencies:

```bash
npm install
```

---

### 3. Environment Setup

Create a `.env` file in the root directory with the following:

```env
DATABASE_URL="your_postgres_connection_string"
NEXTAUTH_SECRET="your_secret_key"
NEXTAUTH_URL="http://localhost:3000"
```

If using Vercel/Neon Postgres:

```env
POSTGRES_PRISMA_URL="..."
POSTGRES_URL_NON_POOLING="..."
```

---

### 4. Database Setup (Prisma)

Run migrations and generate Prisma client:

```bash
npx prisma migrate dev
npx prisma generate
```

Seed the database:

```bash
npx prisma db seed
```

Default test account:

```
Email: john@foo.com
Password: changeme123
```

---

### 5. Run the Application

Start the development server:

```bash
npm run dev
```

Open in browser:

```
http://localhost:3000
```

---

### 6. Run Playwright Tests

Run end-to-end tests:

```bash
npx playwright test
```
Available tests are located in the tests folder.

---

### 7. Project Structure Overview

```
src/
├── app/
│   ├── courses/
│   ├── srch/
│   ├── curriculum/
│   ├── profile/
│   └── auth/
├── components/
├── lib/
│   ├── prisma.ts
│   └── auth.ts
prisma/
├── schema.prisma
└── seed.ts
tests/
```

---

### 8. Modifying the System

#### Adding a New Page
Create a new route:

```
src/app/<route>/page.tsx
```

#### Modifying Forms

Forms are reusable components:
- CourseForm.tsx
- ObjectiveForm.tsx

To modify:
1. Update form component
2. Update Prisma schema if needed
3. Update corresponding server action

#### Updating Database Models

Edit:

```
prisma/schema.prisma
```

Then run:

```bash
npx prisma migrate dev
npx prisma generate
```

#### Authentication

Authentication is handled in:

```
src/lib/auth.ts
```

Uses NextAuth with credentials provider.

---

## Community Feedback

We are interested in your experience using SRCH Curriculum Builder!  If you would like, please take a couple of minutes to fill out the [SRCH Curriculum Builder Feedback Form](#). <!-- need to build form later -->

## Use Cases

As this system is designed to support realistic instructor workflows, the usual use cases include:

**Course Creation and Alignment**

An instructor creates a new course and defines several learning objectives, such as:

• “Understand ethical implications of AI systems”

• “Understanding design processes behind accessibility”

Each objective will be categorized using Bloom’s Taxonomy.

The instructor then browses the SRCH and identifies relevant topics. As they explore, they attach content to specific learning objectives, forming a structured mapping between goals and materials.

**Curriculum Structuring**

After selecting the relevant topics from the SRCH, the instructor is able to organize it and create a representation of how students will learn those topics from a given course material.

**Content Contribution**

Because the SRCH is actively being developed, there are many gaps in the information. An instructor would be able to identify this need and:

• Create new content

• Add explanations and case studies

• Include appropriate learning objectives and references used from their courses

## Example enhancements

While the initial proposal focuses on core functionality, there are several ways the scope could be expanded:

**Analytics Dashboard**

Track how often content is used, which objectives are most common, and where gaps exist.

**Integration with Learning Platforms**

Since platforms like Lamaku already use Bloom’s Taxonomy, this system could integrate directly with assignment creation tools. Additionally, integration with Zotero or other like systems into the search functionality will assist with expanding the knowledge base and decreasing any gaps.

Future versions could include synchronization with an external SRCH database, allowing content to be updated dynamically while preserving instructor-specific mappings.

**Collaborative Curriculum Design**

Allow for the ability to share information between instructors, allowing for one to implement course alignments and mappings already integrated with the SRCH (acting like a similar functionality of sharing a repository structure in GitHub).

## Conclusion

This project addresses a real challenge in modern computing education: aligning new content with structured learning goals. By combining the wider knowledge data pool with the tools proposed into a single platform, this system has the potential to significantly improve how instructors engage with educational resources. Rather than forcing instructors to adapt content found elsewhere into their courses, this tool helps them to shape content around their objectives.

## Team

BowFolios is designed, implemented, and maintained by [Jaimes Mexia-Santiago](https://jmexias.github.io/), [Ahnasia Goulbourne](https://ahnasiakg2234.github.io/), and [Zackary Lown](https://zacklown.github.io/).

<a href="https://docs.google.com/document/d/18CNi7wyIuc5msmWvYp0cfrgZYB2pT_O6dbEzotG73iE/edit?tab=t.0">
  Team Contract Document
</a>

## Development History
* [M1](https://github.com/orgs/manoa-srch/projects/1/views/2)
* [M2](https://github.com/orgs/manoa-srch/projects/6)
* [M3](https://github.com/orgs/manoa-srch/projects/7)
* [Manoa SRCH](https://srch-application-project-eight.vercel.app/)

## In-Progress Implementations to come:
* [Community Feedback](#community-feedback)
* [Developer Guide](#developer-guide)
* [Example enhancements](#example-enhancements)
