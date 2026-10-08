# TalentSignal: Labour Market Intelligence

A job-market analysis toolkit for data and AI roles: which skills are in demand, which come with a salary premium (compared inside the same role), which are rising, which appear together, and how a person's own skills match each role. An AI-written briefing turns the numbers into career advice.

Built in Google Colab with Groq (`openai/gpt-oss-120b`).

> **The 5,000 job postings are made up.** Patterns such as "LLM demand is rising" or "RAG carries a premium" were written into the data generator, so the results demonstrate the **method**, not the real job market. To get real findings, upload a real `job_postings.csv` and edit the column map at the top of the notebook (columns needed: title, city, salary in LPA, minimum experience, skills, posted date).

## What it does

1. **Demand:** postings by role and the share of postings asking for each skill.
2. **Salary by role and city.**
3. **Skill salary premium, compared inside the same role.** A skill's raw premium mixes roles (AI Engineers earn more *and* know LangChain). So the notebook also reports the premium **within the same role**, which is much smaller and more honest.
4. **Rising and falling skills,** comparing the first three months with the last three.
5. **Skill co-occurrence heatmap:** which skills appear together.
6. **Skill gap:** edit `my_skills` and see, for each role, the match percentage and the missing skills. A skill counts as "important" for a role if at least 25% of that role's postings ask for it.
7. **Fresher-friendly share:** postings that ask for 0 years of experience.
8. **AI career briefing (Groq):** told to weigh both demand and salary premium, to avoid saying a skill *causes* higher pay, and to say once that the data is made up.

## Results from the run (made-up data)

| Measure | Result |
|---|---|
| Postings / roles | 5,000 / 6 |
| Most postings | Data Analyst (1,444), Data Scientist (1,015), AI Engineer (718) |
| Median salary by role | AI Engineer 28.0 LPA, ML Engineer 24.4, Data Engineer 19.9, Data Scientist 18.9, BI Developer 11.3, Data Analyst 9.0 |
| Top skills (share of postings) | Python 59.0%, SQL 50.9%, Statistics 32.6%, Machine Learning 29.6%, Power BI 27.2% |
| Fresher-friendly postings | 20.4% |

**Raw vs within-role salary premium (LPA):**

| Skill | Raw gap | Within the same role |
|---|---|---|
| RAG | 11.7 | 2.5 |
| LangChain | 12.8 | 1.7 |
| Docker | 12.2 | 0.9 |
| LLM | 5.8 | 2.5 |
| DAX | -6.5 | +0.3 |

The raw numbers mostly show *which role* a skill belongs to, not extra pay.

**Rising and falling skills:** LLM rose from 16.6% to 31.5% of postings (+14.9 points), RAG +5.4, while Airflow fell 2.6 points. (These trends were written into the generator.)

**Role match for the sample skill list** (Python, SQL, Power BI, Excel, Pandas, Machine Learning, Statistics, LangChain, RAG): Data Analyst 71% (missing Tableau, LLM), Data Scientist 71% (missing Deep Learning, LLM), AI Engineer 67%, BI Developer 50%, ML Engineer 33%, Data Engineer 33%.

## What the evaluation showed

- **Always compare pay inside the same role.** Skipping that step turned a 0.9 LPA effect (Docker) into an apparent 12.2 LPA effect.
- **Demand and premium are different questions.** A skill can be asked for in many postings and still carry little extra pay (Git: 0.5 LPA), or carry a premium but appear rarely.
- **An earlier version had a flaw:** it added "Git, Communication, Cloud" to every role equally, which made Git the top skill and the AI briefing advised learning it first. The generic skills are now rare, so the ranking is driven by role skills.

## Limitations

- **Made-up data.** Do not quote these numbers as facts about the market.
- Even the within-role premium is a signal, not proof that a skill causes higher pay (experience and company type also matter).
- The skill-gap match uses a simple rule (important = asked by 25% or more of a role's postings).
- Skills are matched by text, so spelling variants ("PowerBI" vs "Power BI") would need cleaning on real data.

## Tech stack

pandas, matplotlib, seaborn, Groq API.

## How to run

1. Open the notebook in Google Colab.
2. Run the cells from top to bottom.
3. When asked, paste your own Groq API key (free at console.groq.com). It is hidden while typing and is never saved in the notebook.
4. For real postings, upload `job_postings.csv` and edit `column_map` at the top of Step 3.

## Files the notebook creates

- `talentsignal_jobs.csv`: the postings
- `talentsignal_skills_long.csv`: one row per posting and skill
- `talentsignal_skill_premium.csv`: raw and within-role premiums

---

Built by **Akshat Kesharwani** | [GitHub](https://github.com/akshatkesharwani-info) | [Portfolio](https://akshatkesharwani-info.github.io/)
