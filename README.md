# Activity Points Management System (APMS)

An interactive, responsive front-end web application developed using **React.js** for college students to track, claim, and manage activity points earned through co-curricular, extra-curricular, technical, sports, cultural, and social activities required for degree completion.

---

## 🔗 Project Links

- **GitHub Repository:** [https://github.com/alfredjohnkott-sudo/activity-points](https://github.com/alfredjohnkott-sudo/activity-points)
- **Live Deployment (GitHub Pages):** [https://alfredjohnkott-sudo.github.io/activity-points/](https://alfredjohnkott-sudo.github.io/activity-points/)

---

## 📌 Project Overview & Key Features

This application implements all core requirements specified in the assignment without requiring a backend server or database:

1. **🔐 Student Login Page (`/login`)**
   - Validates student UID and password against pre-configured student records in `src/data/students.json`.
   - Includes quick-access demo credentials buttons to log in with sample accounts instantly.
   - Secure input with password visibility toggling and friendly validation errors.

2. **📊 Student Dashboard (`/`)**
   - Displays student name, UID, department, semester, and academic year.
   - Key metric cards:
     - **Total Activity Points Earned** (sum of officially approved points)
     - **Required / Target Points** (100 points minimum graduation requirement)
     - **Remaining Points** (calculated dynamically: $\max(0, \text{Target} - \text{Earned})$)
     - **Pending Review Points** (activities awaiting faculty coordinator review)
   - Overall visual graduation progress bar with milestone checkpoints (0, 25, 50, 75, 100 Pts).
   - Category-wise points distribution bars with category maximum caps.
   - Recent activity list with status indicators and click-to-view details modal.

3. **📋 Activity List (`/activities`)**
   - Full tabular view of student activities showing Activity ID, Title, Category, Date, Points Claimed, Points Approved, and Status (`Approved`, `Pending`, `Rejected`).
   - Filter by status tabs (`All`, `Approved`, `Pending`, `Rejected`) with live item counts.
   - Category filter dropdown and keyword search (searches title, description, and ID).
   - Multi-option sorting (Newest first, Oldest first, Highest points, Lowest points).
   - Interactive modal popup with full activity audit trail, date, evaluator name, and remarks.

4. **➕ Add Activity Form (`/add-activity`)**
   - Form fields: Activity Title, Category selector, Date of Activity, Points Claimed, Description, and Certificate/Proof identifier.
   - Live category guideline card displaying category description, maximum points allowable, point ranges, and qualifying examples.
   - Comprehensive client-side validation (ensures points claimed do not exceed category maximums).
   - Submissions are added to the student's records with `Pending` status and stored locally.

5. **📁 Activity Categories Showcase (`/categories`)**
   - Displays all 6 recognized activity categories:
     - **Technical & Professional Activities** (Max 40 Pts)
     - **Sports & Athletics** (Max 30 Pts)
     - **Cultural & Fine Arts** (Max 30 Pts)
     - **Social Service & Community** (Max 30 Pts)
     - **Entrepreneurship & Innovation** (Max 35 Pts)
     - **Leadership & Management** (Max 25 Pts)
   - Shows student's current progress in each category against the category limit.
   - Direct shortcuts to claim points in specific categories.

6. **👤 Student Profile (`/profile`)**
   - Institutional Student ID card card featuring photo, UID, department, semester, batch, email, and phone.
   - Overall Summary of Activity Points scorecard.
   - Category-wise activity points audit table with completion percentages.
   - Official graduation eligibility status check (`Requirements Met` vs `In Progress`).
   - "Print Summary Transcript" feature (`window.print()`).
   - Reset button to restore default sample data at any time.

---

## 🛠️ React Concepts & Architecture

- **Component Hierarchy:** Modular, reusable UI components (`Navbar`, `StatusBadge`, `ActivityDetailsModal`, etc.).
- **JSX & Conditional Rendering:** Dynamic badges, conditional review remarks, status counters, and alerts.
- **Props & State Management:**
  - `useState` for local form state, modal triggers, filters, searches, and sort options.
  - `useEffect` for syncing records with browser storage and managing keyboard event listeners.
  - `useMemo` for optimized point calculations, category aggregations, and filtered queries.
- **Context API:**
  - `AuthContext`: Centralized authentication, active student profile, and sample login lookup.
  - `ActivityContext`: Manages activities state, category definitions, points computation, and persistence.
- **React Router:** `HashRouter` is utilized to ensure seamless routing on static hosting environments like GitHub Pages without 404 reload issues.
- **Form Handling & Validation:** Controlled form components with inline errors and point limit safeguards.

---

## 🗄️ JSON Data Architecture

The project relies purely on structured JSON data stored in `src/data/`:
- `src/data/students.json`: Student profiles, credentials, departments, semesters, and targets.
- `src/data/categories.json`: Official category definitions, descriptions, point caps, and guidelines.
- `src/data/activities.json`: Sample completed, pending, and reviewed student activity records.

---

## 👥 Demo Student Credentials

| Student Name | Student UID | Password | Department | Semester |
| :--- | :--- | :--- | :--- | :--- |
| **Alfred John** (Default) | `STU2023CS042` | `password123` | Computer Science & Engg | 6th Semester |
| **Sarah Miller** | `STU2023EC018` | `password123` | Electronics & Comm | 4th Semester |
| **David Chen** | `STU2023ME091` | `password123` | Mechanical Engineering | 8th Semester |

*(Tip: On the login page, you can also click any of the student demo badges to auto-fill credentials instantly).*

---

## 🚀 How to Run the Application Locally

### Prerequisites
- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- [npm](https://www.npmjs.com/)

### Step 1: Clone the Repository
```bash
git clone https://github.com/alfredjohnkott-sudo/activity-points.git
cd activity-points
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Start the Development Server
```bash
npm run dev
```
Open your browser and navigate to the local URL displayed (typically `http://localhost:5173/`).

### Step 4: Build for Production
```bash
npm run build
```
The production bundle will be generated in the `dist/` folder.

---

## 🌐 Deployment to GitHub Pages

### Method 1: Automatic via GitHub Actions (Recommended)
This repository includes a pre-configured workflow in `.github/workflows/deploy.yml`.
1. Push your code to the `main` branch:
   ```bash
   git add .
   git commit -m "Initial release of Activity Points Management System"
   git push origin main
   ```
2. In your GitHub repository, navigate to **Settings > Pages**.
3. Under **Build and deployment > Source**, select **GitHub Actions**.
4. GitHub Actions will build and deploy the application automatically to `https://alfredjohnkott-sudo.github.io/activity-points/`.

### Method 2: Manual deployment using `gh-pages`
```bash
npm run deploy
```
This runs `npm run build` and automatically pushes the contents of `dist/` to the `gh-pages` branch.

---

## 📁 Project Directory Structure

```
activity-points/
├── .github/
│   └── workflows/
│       └── deploy.yml          # Automated GitHub Pages CI/CD workflow
├── public/
│   └── vite.svg
├── src/
│   ├── components/
│   │   ├── ActivityDetailsModal.jsx  # Activity popup modal
│   │   ├── Navbar.jsx                # Responsive top navigation bar
│   │   └── StatusBadge.jsx           # Approved / Pending / Rejected badge
│   ├── context/
│   │   ├── ActivityContext.jsx       # Activity data & point calculations
│   │   └── AuthContext.jsx           # Student login & session state
│   ├── data/
│   │   ├── activities.json           # Sample activity entries
│   │   ├── categories.json           # Activity categories & point limits
│   │   └── students.json             # Sample student records & credentials
│   ├── pages/
│   │   ├── ActivityListPage.jsx      # Filterable & searchable activities
│   │   ├── AddActivityPage.jsx       # Activity submission form
│   │   ├── CategoriesPage.jsx        # Categories & rules overview
│   │   ├── DashboardPage.jsx         # Summary metrics & recent activities
│   │   ├── LoginPage.jsx             # UID / password login screen
│   │   └── ProfilePage.jsx           # Student ID & points audit
│   ├── App.jsx                       # Application routes & layout
│   ├── index.css                     # Global design & responsive styling
│   └── main.jsx                      # App root with HashRouter & Providers
├── index.html                        # HTML entry point
├── package.json                      # Project metadata & scripts
├── vite.config.js                    # Vite configuration
└── README.md                         # Project documentation
```

---

## 📝 License
This project was developed for the **Web Programming Assignment - Activity Points Management System**.
