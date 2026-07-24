# 🎓 Smart Study Buddy

*Building AI course project*

## 📝 Summary

Smart Study Buddy is an AI-powered learning assistant that creates personalized study plans, predicts exam performance, and recommends optimal study resources based on individual learning patterns, past performance, and time availability.

## 🎯 Background

### Problems Solved:
- **Information overload**: Students don't know what to study first
- **Inefficient studying**: Many students waste time on topics they already know
- **Exam anxiety**: Students have no idea how prepared they really are
- **One-size-fits-all education**: Traditional methods ignore individual learning styles

### Motivation:
- 65% of students report feeling overwhelmed by exam preparation
- Personalized learning can improve retention by up to 60%
- This project democratizes access to AI-powered tutoring

## 💡 How It Works

### User Flow:
1. **Student logs in** and inputs their subjects/topics
2. **System analyzes** past performance (grades, time spent, difficulty levels)
3. **AI generates** personalized study schedule
4. **Student tracks** progress daily
5. **AI adjusts** recommendations based on performance

### Key Features:
- Personalized study schedule generator
- Intelligent topic prioritization
- Performance prediction engine
- Progress tracking dashboard
- Resource recommendation (videos, articles, exercises)

![Smart Study Buddy Flowchart](images/flowchart.png)

### Sample Code

```python
class SmartStudyBuddy:
    def __init__(self, student_data):
        self.student = student_data
        self.study_plan = []
        self.performance_history = []
    
    def generate_study_plan(self, upcoming_exams, available_hours):
        """
        Creates personalized study schedule
        """
        for exam in upcoming_exams:
            difficulty = self.assess_difficulty(exam)
            mastery = self.get_current_mastery(exam)
            priority = self.calculate_priority(difficulty, mastery)
            
            allocated_time = self.allocate_time(
                priority, 
                available_hours
            )
            
            self.study_plan.append({
                'topic': exam,
                'hours': allocated_time,
                'priority': priority,
                'resources': self.recommend_resources(exam)
            })
        return self.study_plan

    def predict_performance(self, hours_studied, topic):
        """
        Predicts exam score based on study time
        """
        # Linear regression model
        current_mastery = self.get_current_mastery(topic)
        improvement_rate = self.get_learning_rate(topic)
        predicted_score = min(
            100, 
            current_mastery + (hours_studied * improvement_rate)
        )
        return predicted_score

    def recommend_resources(self, topic):
        """
        Suggests best study materials
        """
        resources = {
            'videos': [],
            'articles': [],
            'exercises': []
        }
        
        # Collaborative filtering based on similar students
        similar_students = self.find_similar_students()
        best_resources = self.get_top_resources(similar_students, topic)
        
        return best_resources

def main():
    # Create student profile
    student = {
        'id': 'STU001',
        'grade': '10th',
        'subjects': ['Math', 'Physics', 'Biology'],
        'current_scores': {'Math': 78, 'Physics': 65, 'Biology': 82},
        'learning_style': 'visual'
    }
    
    # Initialize Smart Study Buddy
    buddy = SmartStudyBuddy(student)
    
    # Generate study plan
    exams = ['Math Exam', 'Physics Exam']
    study_plan = buddy.generate_study_plan(exams, available_hours=20)
    
    print("📚 Your Personalized Study Plan:")
    print("=" * 40)
    for session in study_plan:
        print(f"📘 {session['topic']}")
        print(f"   ⏰ Hours: {session['hours']}")
        print(f"   📊 Priority: {session['priority']}")
        print("-" * 30)

main()
