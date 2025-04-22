# Product Requirements Document (PRD) - NPCstorage

## 1. Product Overview
NPCstorage is a web-based application designed for Game Masters (GMs) of the 2nd edition of Warhammer Fantasy Roleplay (WHFRP). Its primary goal is to streamline the process of creating and managing Non-Player Characters (NPCs). The Minimum Viable Product (MVP) will focus on providing tools for manual NPC entry, random NPC generation based on user-specified experience points (XP), editing capabilities, persistent storage of NPCs linked to user accounts, and a basic system for managing temporary statistical changes during gameplay. The application aims to save GMs time during preparation and provide quick access to NPC data during sessions. The primary language for the UI and core data will be Polish.

## 2. User Problem
Manually creating stats for NPCs in pen-and-paper RPGs, specifically WHFRP 2e, is a time-consuming process involving repetitive tasks like rolling for attributes and looking up career details. Furthermore, storing NPC information on physical paper makes it difficult to quickly and conveniently access their data, especially during active game sessions. This hinders efficient gameplay and increases GM workload.

## 3. Functional Requirements
- **FR-001**: System Compatibility: The application must be compatible with the ruleset of Warhammer Fantasy Roleplay 2nd Edition.
- **FR-002**: Manual NPC Creation: Users must be able to manually create a new NPC by entering all relevant statistics, skills, talents, appearance details, backstory, etc.
- **FR-003**: Random NPC Generation:
    - **FR-003a**: The system must allow users to initiate random NPC generation.
    - **FR-003b**: Users must be able to specify a total amount of Experience Points (XP) for the generated NPC.
    - **FR-003c**: Users must have the option to select a specific Race or allow the system to choose one randomly according to WHFRP 2e rules.
    - **FR-003d**: The system must randomly roll base statistics according to WHFRP 2e rules for the chosen/randomized Race.
    - **FR-003e**: Users must be prompted to select an initial valid career path for the NPC.
    - **FR-003f**: The system must automatically spend the user-provided XP according to the rules of the selected career path(s) and WHFRP 2e advancement rules.
    - **FR-003g**: When a career path's advancements are fully purchased with the available XP, and if further valid career options ('profesje wyjściowe') exist according to imported data, the user must be prompted via a pop-up to choose the next career. This process repeats until XP is spent or no valid progression is possible.
    - **FR-003h**: The system must use an LLM (e.g., Ollama) to generate a 4-7 sentence character description in Polish based on the NPC's Race, Career Path, and specific Appearance fields (`Wzrost`, `Waga`, `Kolor Włosów`, `Kolor oczu`, `Znaki szczegulne`, `Znak gwiezdny`, `Miejsce pochodzenia`, `Wiek`, `Liczba rodzeństwo`).
- **FR-004**: NPC Editing: Users must be able to edit *any* field (stats, skills, talents, appearance, story, etc.) of any NPC (manually created or randomly generated) at any time after its creation.
- **FR-005**: NPC Persistence:
    - **FR-005a**: The system must provide user registration and login functionality.
    - **FR-005b**: Created and saved NPCs must be associated with the user's account.
    - **FR-005c**: Saved NPCs must be persistent and accessible to the user after logging out and logging back in.
    - **FR-005d**: System must provide change password and delete account functionality.
- **FR-006**: NPC List View:
    - **FR-006a**: The application must display a list of all NPCs saved by the logged-in user.
    - **FR-006b**: The list view must support sorting based on NPC Name, Race, and Profession.
    - **FR-006c**: The list view must support filtering based on NPC Name, Race, and Profession.
    - **FR-006d**: The list view must support free-text searching based on NPC Name, Race, and Profession.
- **FR-007**: Temporary Effects Management:
    - **FR-007a**: Users must be able to apply a temporary modifier (positive or negative) to any specific statistic of an NPC.
    - **FR-007b**: Active temporary modifiers must be clearly indicated on the NPC's character sheet view (e.g., highlighted values).
    - **FR-007c**: Users must be able to view a list of all currently active temporary effects on an NPC.
    - **FR-007d**: Users must be able to remove specific temporary effects individually.
    - **FR-007e**: Users must be able to remove all active temporary effects simultaneously.
- **FR-008**: Data Import: The system must be able to parse and import data from predefined CSV files containing information for Careers, Skills, and Talents. These files will be in Polish.
    - **FR-008a**: Career CSV: Must include name, advancement stats, skills, talents, 'profesje wyjściowe'.
    - **FR-008b**: Skill CSV: Must include name, governing statistic, description.
    - **FR-008c**: Talent CSV: Must include name, description.
- **FR-009**: CSV Error Handling:
    - **FR-009a**: If a skill or talent entry in a CSV is missing a description, it should be imported with placeholder text for the description.
    - **FR-009b**: If a skill or talent entry in a CSV is missing a name, it should be imported with placeholder text for the name.
    - **FR-009c**: If a career entry in a CSV references a non-existent next career ('profesje wyjściowe'), the error should be logged, and that specific invalid career path option must not be presented to the user during generation/progression.
- **FR-010**: Language: The primary user interface language and the language for core data (imported skills, talents, careers) must be Polish.

## 4. Product Constraints
- **PC-001**: Platform: The application will be web-based only. No mobile application is planned for the MVP.
- **PC-002**: System Scope: Compatibility is strictly limited to Warhammer Fantasy Roleplay 2nd Edition for the MVP. Other systems (e.g., WHFRP 4e, D&D 5e) are excluded.
- **PC-003**: Feature Scope (Exclusions):
    - **PC-003a**: Advanced NPC organization features (e.g., tagging systems) are excluded from the MVP.
    - **PC-003b**: NPC sharing features between users are excluded from the MVP.
    - **PC-003c**: Direct integration of skill/talent mechanics with character stat mechanics (e.g., automatic calculation of test chances) is excluded from the MVP.
    - **PC-003d**: Automatic tracking of temporary effect durations (e.g., number of rounds) is excluded from the MVP; removal is manual.
    - **PC-003e**: Explicit features for balancing NPC stats are excluded from the MVP (though editing capability allows manual balancing).
- **PC-004**: Technical Dependencies: The application requires a backend database for storing user and NPC data, avaiable professions, skills and talents, and access to an LLM API (Ollama considered) for character description generation.
- **PC-005**: Language: The primary language for UI and core data is Polish. LLM must be capable of processing inputs and generating outputs in Polish.

## 5. User Stories

---
**US-001**
Title: User Registration
Description: As a new user, I want to register an account using an email and password, so that I can save my created NPCs and access them later.
Acceptance Criteria:
- User can navigate to a registration page/form.
- User provides a valid email address and a password meeting minimum security requirements.
- Upon successful submission, a new user account is created in the system.
- User receives confirmation of successful registration.
- User is automatically logged in or redirected to the login page.
- System validates email format.
- System checks if the email is already registered.

---
**US-002**
Title: User Login
Description: As a registered user, I want to log in to my account using my email and password, so that I can access my saved NPCs and use the application's features.
Acceptance Criteria:
- User can navigate to a login page/form.
- User enters their registered email and correct password.
- Upon successful authentication, the user is granted access to their dashboard/NPC list.
- If authentication fails (incorrect email/password), an appropriate error message is displayed.
- Session management ensures the user remains logged in until they explicitly log out or the session expires.

---
**US-003**
Title: Initiate Random NPC Generation
Description: As an Advanced GM, I want to start the process of generating a random WHFRP 2e NPC, specifying the total XP, so I can quickly create a character based on points.
Acceptance Criteria:
- User can find and activate a "Generate Random NPC" function.
- User is prompted to enter a non-negative integer value for total XP.
- User has the option to select a specific Race from a list valid for WHFRP 2e, or choose "Random".
- User confirms choices to proceed with generation.

---
**US-004**
Title: Select Initial Career Path
Description: As an Advanced GM generating an NPC, I want to choose the starting career path after the system rolls stats, so I can guide the character's initial development.
Acceptance Criteria:
- After Race and XP are set and stats are rolled (implicitly), the user is presented with a list of valid starting career paths based on WHFRP 2e rules.
- User can select one career path from the list.
- The system proceeds to spend XP based on the selected career.

---
**US-005**
Title: Select Subsequent Career Path
Description: As an Advanced GM generating an NPC, if my current career is maxed out and XP remains, I want to be prompted to choose the next career from valid options ('profesje wyjściowe'), so the character can progress realistically.
Acceptance Criteria:
- When the system finishes spending XP on the current career's advancements, it checks if XP remains and if valid 'profesje wyjściowe' exist in the imported career data.
- If both conditions are true, a pop-up appears listing the valid next career options.
- Only careers listed as 'profesje wyjściowe' for the completed career AND existing in the imported data are shown.
- Invalid paths (due to CSV errors, as per FR-009c) are not presented.
- User selects one career from the pop-up list.
- The system continues spending the remaining XP on the newly selected career.
- If no valid options exist or no XP remains, the generation process regarding career progression concludes.

---
**US-006**
Title: View Generated NPC Details
Description: As an Advanced GM, after the random generation process is complete, I want to view the full details of the generated NPC, including stats, skills, talents, and the LLM-generated description, so I can review the result.
Acceptance Criteria:
- Upon completion of the generation process (including XP spending and description generation), the full character sheet is displayed.
- All calculated stats, assigned skills/talents based on career and XP spend, are visible.
- The generated Polish character description (4-7 sentences) is displayed.
- All appearance fields are displayed.
- The user has options to Edit or Save the NPC.

---
**US-007**
Title: Manually Create NPC
Description: As an Advanced GM, I want to manually create a new NPC by filling in all their details (stats, skills, talents, story, etc.), so I have full control over specific characters.
Acceptance Criteria:
- User can find and activate a "Create Manual NPC" function.
- User is presented with a blank character sheet form containing all necessary fields (Stats, Skills, Talents, Appearance, Bio, etc.).
- User can input values into all fields.
- Input validation is present for relevant fields (e.g., numerical stats).
- User can save the manually entered NPC.

---
**US-008**
Title: Edit Existing NPC
Description: As an Advanced GM, I want to edit any aspect of a previously saved NPC (whether generated or manually created), so I can update them as the campaign progresses or correct details.
Acceptance Criteria:
- User can select a saved NPC from their list.
- User can activate an "Edit" mode for the selected NPC.
- All fields on the character sheet become editable.
- User can modify any value (stats, skills, talents, text fields, etc.).
- User can save the changes made to the NPC.
- User can cancel the edits without saving.

---
**US-009**
Title: Save NPC
Description: As an Advanced GM, after generating or manually creating/editing an NPC, I want to save the NPC to my account, so I can access it later.
Acceptance Criteria:
- A "Save" button/option is available when viewing a newly generated or edited NPC.
- Clicking "Save" persists the current state of the NPC data to the database, associated with the logged-in user's account.
- The user receives confirmation that the NPC was saved successfully.
- The saved NPC appears in the user's NPC list.

---
**US-010**
Title: View NPC List
Description: As an Advanced GM, I want to view a list of all NPCs I have previously saved, so I can easily find and select them.
Acceptance Criteria:
- User can navigate to a dedicated "My NPCs" or "NPC List" section.
- The section displays a list/table of all NPCs associated with the user's account.
- Key information like Name, Race, and Profession is visible for each NPC in the list.

---
**US-011**
Title: Search NPC List
Description: As an Advanced GM, I want to search my list of saved NPCs by Name, Race, or Profession using free text, so I can quickly find a specific character.
Acceptance Criteria:
- A search input field is available on the NPC list view.
- User enters text into the search field.
- The list dynamically updates to show only NPCs where the Name, Race, or Profession matches the search term (case-insensitive partial match).
- Clearing the search field restores the full list (respecting any active filters/sort order).

---
**US-012**
Title: Filter NPC List
Description: As an Advanced GM, I want to filter my list of saved NPCs based on pre-defined criteria like Race or Profession, so I can narrow down the list to relevant characters.
Acceptance Criteria:
- Filtering options (e.g., dropdowns, checkboxes) for Race and Profession are available on the NPC list view.
- User selects filter criteria.
- The list updates to show only NPCs matching the selected filter(s).
- Multiple filters can be applied simultaneously (e.g., filter by Race AND Profession).
- Filters can be cleared to show the full list (respecting search/sort order).

---
**US-013**
Title: Sort NPC List
Description: As an Advanced GM, I want to sort my list of saved NPCs by Name, Race, or Profession (ascending/descending), so I can organize the view according to my needs.
Acceptance Criteria:
- Sorting controls (e.g., clickable column headers) for Name, Race, and Profession are available on the NPC list view.
- Clicking a sort control sorts the list based on that field.
- Clicking the same control again reverses the sort order (ascending/descending).
- The current sort order is visually indicated.

---
**US-014**
Title: View Specific NPC Details
Description: As an Advanced GM, I want to select an NPC from my list and view their full character sheet, so I can access their details during a game session.
Acceptance Criteria:
- User can click on an NPC entry in the list view.
- Clicking navigates the user to the detailed character sheet view for that specific NPC.
- All saved details (stats, skills, talents, description, etc.) are displayed accurately.
- Temporary effects (if any) are visibly highlighted.

---
**US-015**
Title: Apply Temporary Stat Modifier
Description: As an Advanced GM, during a session, I want to apply a temporary modifier (e.g., +10 WS, -5 Ag) to an NPC's statistic, so I can track in-game effects like spells or conditions.
Acceptance Criteria:
- When viewing an NPC's sheet, a "Temporary Change" or similar button is available.
- Clicking the button opens a modal or form.
- User selects the target statistic from a list.
- User enters a numerical modifier value (positive or negative).
- User confirms the change.
- The change is applied, and the affected statistic on the character sheet is updated and visually highlighted (e.g., color change, icon).
- The temporary modifier is stored temporarily (for the session or until removed).

---
**US-016**
Title: View Active Temporary Modifiers
Description: As an Advanced GM, I want to see a summary of all active temporary modifiers currently affecting an NPC, so I know what effects are in play.
Acceptance Criteria:
- An option (e.g., "View Temporary Effects", "Unset Temporary Changes" button leading to a list) is available on the NPC sheet.
- Activating this option displays a list/modal showing all currently active temporary modifiers.
- Each entry in the list clearly shows the affected statistic and the modifier value (e.g., "WS: +10", "Ag: -5").

---
**US-017**
Title: Remove Specific Temporary Modifier
Description: As an Advanced GM, I want to be able to remove a single, specific temporary modifier from an NPC when the effect ends, so their stats return to normal accurately.
Acceptance Criteria:
- In the view showing active temporary modifiers (see US-016), each effect has a corresponding "Remove" or "Delete" option.
- User clicks the remove option for a specific effect.
- The selected temporary modifier is removed.
- The NPC's affected statistic on the character sheet returns to its value prior to that specific modifier (considering other active modifiers).
- The effect is removed from the list of active modifiers.

---
**US-018**
Title: Remove All Temporary Modifiers
Description: As an Advanced GM, I want a quick way to remove all active temporary modifiers from an NPC at once (e.g., end of combat), so I can reset their stats efficiently.
Acceptance Criteria:
- In the view showing active temporary modifiers (see US-016), an "Remove All" or "Clear All Effects" option is available.
- User clicks the "Remove All" option.
- A confirmation prompt may appear.
- Upon confirmation, all active temporary modifiers are removed from the NPC.
- All affected statistics on the character sheet revert to their base values.
- The list of active modifiers becomes empty.

---
**US-019**
Title: View LLM Generated Description
Description: As an Advanced GM, when viewing a randomly generated NPC, I want to see the unique character description created by the LLM, so I can get inspiration for their personality and background.
Acceptance Criteria:
- The LLM-generated description (as per FR-003h) is displayed in a dedicated section on the character sheet for randomly generated NPCs.
- The description is in Polish and is 4-7 sentences long.
- The description reflects the NPC's Race, Career Path, and relevant appearance details.

---
**US-020**
Title: Handle Missing CSV Skill/Talent Data
Description: As a System Administrator/Developer, I need the system to handle errors gracefully when parsing Skill or Talent CSVs that have missing data, so the import process doesn't fail completely.
Acceptance Criteria:
- When parsing Skill/Talent CSVs:
    - If a 'description' field is empty, the skill/talent is imported, and the description attribute is set to a predefined placeholder text (e.g., "Brak opisu / No description").
    - If a 'name' field is empty, the skill/talent is imported, and the name attribute is set to a predefined placeholder text (e.g., "Brak nazwy / No name").
- The import process continues for other valid entries in the file.

---
**US-021**
Title: Handle Invalid Career Path Data
Description: As a System Administrator/Developer, I need the system to handle errors when a Career CSV entry lists an invalid 'profesje wyjściowe', so users aren't presented with broken progression options.
Acceptance Criteria:
- When parsing Career CSVs:
    - If a career listed in 'profesje wyjściowe' does not correspond to a valid career name also present in the imported career data, this specific invalid path is flagged.
    - An error or warning message detailing the invalid path reference is logged by the system.
    - During random NPC generation (US-005), this specific invalid career path is *not* presented to the user as a selectable option, even if listed in the source CSV.
- The import process continues for other valid entries and career paths.

---

## 6. Success Metrics
- **SM-001**: User Adoption & Engagement (Primary): At least 75% of registered users successfully save at least one created NPC (either manually created or randomly generated). Measurement: Track the percentage of user accounts with >= 1 saved NPC record in the database.
- **SM-002**: Core Functionality - Generation: Successful completion rate of the random NPC generation process (from initiation to displaying the final NPC sheet with description). Measurement: Monitor application logs for successful generation events vs. errors during the process. Target > 99%.
- **SM-003**: Core Functionality - Persistence: NPCs are successfully saved and retrieved across user sessions. Measurement: Automated tests verifying save/load functionality; monitoring for data loss issues. Target: Zero critical data loss incidents.
- **SM-004**: Core Functionality - Editing & Viewing: Users can successfully view, edit, and save changes to NPCs. Measurement: Monitoring for errors during edit/save operations. Qualitative feedback on ease of use.
- **SM-005**: Qualitative Feedback: Gather user feedback via surveys or in-app feedback forms post-MVP launch focusing on ease of use, speed of generation/lookup, and the perceived utility of the features. Measurement: Analysis of qualitative feedback themes.