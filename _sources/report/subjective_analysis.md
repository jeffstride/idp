# Subjective Analysis
This report uses the data in the **Correlations to Success** report. Here we attempt to explain *why* correlations exist and *what to do*.  

Ideally, the results of the study would be to identify avenues for instructors and universities to better prepare students for academic success. 

## Abstract
Some of the data can appear to be circular (self-fullfilling). In other words, good students are good students. More specifically, students who have a high GPA are likely to get a better grade in CSS 143. Students who experienced success in CSS 142 are more likely to experience success in CSS 143. Students who found the subject matter to be easy more easily succeeded. These are all essentially saying, *"Good students are good students."* Nevertheless, there is opportunity to improve students' chances of success through some activities such as: improving attendance, fostering peer connections, and promoting resilience. Further study needs to happen to:  
1) validate the correlations by repeating parts of the study 
2) see if extrinsic factors that increase the Advantaged Feature count can actually improve student performance  
3) see if equally strong correlations can be determined before the student even begins the course    

## Analysis
The <a href="#ai-analysis-of-report">below</a> is what AI composed from the report. I believe that the suggestions are naive and assume too much causality in the correlations.   

I have some suspicions (and data) about how or why some features would contribute to a better grade in 143.  

### Friends
There are 3 reasons why more friends promotes better performance:  
1) **Average of 5:** You are the average of the five people you spend the most time with.  
2) **Academic Dishonesty:** More friends in a class gives you more ways to get insider information and an unfair advantage on the homework and exams. 
3) **More Support:** More friends in a class gives you more support and resources.  
 
### More Friends --> More Academic Dishonesty
Students who have more friends are more likely to get *"Black Market"* copies of prior exams and insider information on the exams. The more access you have to an unfair advantage, the more likely you are to use it. To better understand this, allow me to explain how I operated and the data I have.  

During the academic year while conducting this study, I had a total of five sections over three quarters. The first quarter had a single section, and I was completely new to the school. There was hardly any room for academic dishonesty. However, during the second and third quarter, there were two ways to cheat.  
1) Get copies of prior exams  
2) Hear from the earlier section the specifics questions on the exam  

I made two mistakes:  
1) From quarter to quarter, I only marginally updated the multiple choice portion of the exam. While I did not allow students to take exams out of the classroom, and I did my best to prevent students from taking pictures or otherwise stealing the exam.   
2) From section to section in the same quarter, I used the exact same exam. This is the crux of the problem.  

As news spread and students became more aware of how to cheat, the data showing cheating manifested. I also have two pieces of evidence supporting the fact that cheating occurred. 1) One honest student told me that he was offered a copy of last quarter's MCQ. 2) I caught a student with the answers to the FRQ in the later section.  

I don't believe the data shows improved exam scores from quarter to quarter. **(TODO: Show this data.)** This suggests that the exams where either changed enough from quarter to quarter, and/or that any *"black market"* exams had an insignificant impact.    

#### Section Differences
Below you'll see MCQ/FRQ scores and how they changed from section to section.  
Note how the Student-t test shows that the average MCQ is significantly different on every exam. Furthermore, the later section had better performance on every exam. Never did an earlier section do better.  

```
Winter 2025:
Midterm #1: MCQ +0.5%.  FRQ: +1.6%
Midterm #2: MCQ +4.4%   FRQ: +2.6%
Final:      MCQ +1.8%   FRQ: +0.2%

Spring 2025:
Midterm #1: MCQ +10.9%  FRQ: + 4.8%
Midterm #2: MCQ +10.5%  FRQ: +13.2%
Final:      MCQ + 7.3%  FRQ: + 5.6%

MID1      t_stat	p_value	significant	n_A	n_B
FRQ(%)	  0.9851	0.3272	   False	44	45
MCQ(%)	  2.3285	0.0222	    True	44	45
Total(%)  1.8238	0.0716	   False	44	45

MID2	  t_stat	p_value	significant	n_A	n_B
FRQ(%)	  2.3338	0.0221	    True	41	44
MCQ(%)	  2.5990	0.0110	    True	41	44
Total(%)  2.6264	0.0103	    True	41	44

Final	  t_stat	p_value	significant	n_A	n_B
FRQ(%)	  1.0942	0.2775	   False	38	36
MCQ(%)	  2.1645	0.0337	    True	38	36
Total(%)  1.9072	0.0605     False	38	36

```

### Is Multiple Choice a Poor Choice?
The data shows that a bit more cheating occurs on the MCQ. When analyzing the Spring 2025 quarter, the MCQ was significantly (using p=0.05) different across the two sections for all three exams. The FRQ was statistically different for midterm #2, however it was *"noticably"* different across all thee exams.  

An MCQ has many questions. Students leaving an exam could not easily memorize all the questions. However, should a student get their hands on a stolen MCQ, providing correct answers without true knowledge (i.e. memorization) on the subject would be relatively easy. An FRQ would be easier to remember because there are fewer quctions, but it would harder to fake an answer.  

As an instructor, I find it hard to continually author good multiple choice questions that measure real knowledge. 

### Average of 5
The motivational speaker, Jim Rohn, in the 1980's originated the concept that *"you are the average of the five people you spend the most time with."* The people in your inner circle help shape your success, habits, and income. 

A school's program may attempt to increase the count of friends a student has in order to improve their academic success on the premise that more friends gives you more emotional support, more study partners, and a better experience in a program (an experience is undoubtedly better with friends). While I do not contest these as I believe them to be true, I think the greater impact on a student's score originating from a friend group comes from the other two areas: *Average of 5* and *Academic Dishonesty*.  

While there's no study literally calculating the "average" of your five friends, extensive social science shows that our close social circle does influence us. One study<a href="#references"><sup>[1]</sup></a> shows how close firends' and admired peers' academic engagement contributed to their own academic engagement **over time**. It shows that adolescents who were similar in academic engagement more often became friends. It not state that simply having more friends would increase your academic performance. Instead, if your genuine interests are in Computer Science, you are likely to have more friends also in Computer Science: you are more likely to have a genuine and longstanding interest in Computer Science if your friends do. The study does suggest that if your friends are academically strong that you would migrate to become academically strong as well. Through a social contagion you would start to value academics more and strive to become better at academics.  Friends serve to influence your behavior over time.<a href="#references"><sup>[2]</sup></a>   

If any program (e.g. STARS) were to work toward building up a larger friend network, the effort should be to introduce struggling students with high performing students. A friend network including only poor achieving students could perpetuation poor performance.  
   
## AI Analysis of Report
> This section is what AI created, verbatim, about my report.  

The report provides insights into factors that correlate with better performance in CSS 143, which can be leveraged to increase students' advantage count in future courses.  Here are some speculative strategies based on the findings:
1) Improve CSS 142 Preparation:
    * Focus on ensuring students achieve a strong foundation in CSS 142, as higher grades in this course correlate with better performance in CSS 143. 
    * Offer additional resources, tutoring, or review sessions for CSS 142 concepts.
2)	Reduce Perceived Difficulty:
    * Simplify complex concepts or provide more structured guidance to make the course feel less challenging.
    * Incorporate scaffolding techniques to gradually build students' confidence and skills.
3)	Enhance Enjoyment of Coding:
    * Design assignments that are engaging and fun, such as gamified coding challenges or real-world projects.
    * Encourage creativity and exploration in coding tasks.
4)	Foster Peer Connections:
    * Create opportunities for students to form friendships, such as group projects, study groups, or social events.
    * Pair students with peers who have taken the course before for mentorship.
5)	Encourage Regular Attendance:
    * Emphasize the importance of attending class and provide incentives for consistent participation.
    * Make classes interactive and engaging to motivate students to attend.
6)	Support English Fluency:
    * Provide language support for non-native English speakers, such as glossaries for technical terms or additional explanations.
    * Encourage students to practice technical communication skills.
7)	Promote Grit and Resilience:
    * Teach strategies for overcoming challenges, such as debugging techniques or problem-solving frameworks.
    * Share stories of perseverance and success to inspire students.
8)	Increase Exposure to Programming:
    * Offer workshops or extracurricular activities to introduce students to programming before they take CSS 143.
    * Encourage students to explore coding projects outside of class.
9)	Reduce Workload Outside School:
    * Provide flexible deadlines or alternative schedules for students who work long hours.
    * Offer financial aid or scholarships to reduce the need for excessive work hours.
10)	Support First-Generation Students:
    * Provide targeted resources, mentorship, and support for first-generation college students.
    * Create a welcoming and inclusive environment that addresses their unique challenges.
11)	Encourage Independent Coding Projects:
    * Motivate students to work on personal coding projects by showcasing examples and providing guidance.
    * Offer incentives, such as extra credit, for completing independent projects.

By implementing these strategies, instructors can help students build more advantageous features, thereby increasing their advantage count and improving their chances of success in future courses. 

## References
[1] Huiyoung Shin [Social contagion of academic behavior: Comparing social networks of close friends and admired peers](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0265385) Plos 2022.   

[2] McPherson M, Smith-Lovin L, Cook JM. Birds of a feather: Homophily in social networks. Annu Rev Sociol. 2001;27:415–444. https://doi.org/10.1146/annurev.soc.27.1.415