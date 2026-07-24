class SmartStudyBuddy:
    def __init__(self, student_data):
        self.student = student_data
        self.study_plan = []
        self.performance_history = []
    
    def generate_study_plan(self, upcoming_exams, available_hours):
        """
        Creates personalized study schedule based on student data
        """
        for exam in upcoming_exams:
            # Calculate priority based on difficulty and current mastery
            difficulty = self.assess_difficulty(exam)
            mastery = self.get_current_mastery(exam)
            priority = self.calculate_priority(difficulty, mastery)
            
            allocated_time = self.allocate_time(priority, available_hours)
            
            self.study_plan.append({
                'topic': exam,
                'hours': allocated_time,
                'priority': priority,
                'resources': self.recommend_resources(exam)
            })
        return self.study_plan

    def predict_performance(self, hours_studied, topic):
        """
        Predicts exam score using linear regression model
        """
        current_mastery = self.get_current_mastery(topic)
        learning_rate = self.get_learning_rate(topic)
        predicted_score = min(100, current_mastery + (hours_studied * learning_rate))
        return predicted_score

    def recommend_resources(self, topic):
        """
        Recommends study resources using collaborative filtering
        """
        similar_students = self.find_similar_students()
        best_resources = self.get_top_resources(similar_students, topic)
        return best_resources

# Example usage
student = {'id': 'STU001', 'subjects': ['Math', 'Physics', 'Biology']}
buddy = SmartStudyBuddy(student)
study_plan = buddy.generate_study_plan(['Math Exam', 'Physics Exam'], 20)
print(study_plan)
