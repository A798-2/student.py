# student.py
学生教务管理系统

class Student:
    def __init__(self, name, chinese, math, english):
        self.name = name
        self.chinese = chinese
        self.math = math
        self.english = english

    def __str__(self):
        return f"{self.name}的语文{self.chinese},数学为：{self.math},英语成绩为:{self.english}"

    # 如果需要修改成绩：
    def fix_k(self, chinese=None, math=None, english=None):#不能直接赋值为0
        if chinese is not None:
            self.chinese = chinese
        if math is not None:
            self.math = math
        if english is not None:
            self.english = english

# 教务系统
class EduSystem:
    def __init__(self):
        self.student_list = []

    # 1. 添加学生成绩
    def add_student(self):
        name = input("请输入要添加的学生姓名：")
        for s in self.student_list:
            if s.name == name:
                print("该生成绩已经添加")
                return                          # 重名才退出
        chinese = int(input("请输入学生的语文成绩："))
        math = int(input("请输入学生的数学成绩："))
        english = int(input("请输入学生的英语成绩："))
        if 0 <= english <= 100 and 0 <= math <= 100 and 0 <= chinese <= 100:
            stu = Student(name, chinese, math, english)
            self.student_list.append(stu)
            print("成绩符合，可以录入")
        else:
            print("成绩不符合规范，不录取")

    # 2. 修改学生成绩
    def update_student(self):
        name = input("请输入要修改的学生姓名：")
        for s in self.student_list:
            if s.name == name:
                print(f"当前的成绩是：{s}")
                chinese = int(input("请输入新的语文成绩："))
                math = int(input("请输入新的数学成绩："))
                english = int(input("请输入新的英语成绩："))
                if 0 <= chinese <= 100 and 0 <= math <= 100 and 0 <= english <= 100:
                    s.fix_k(chinese, math, english)   # 改原来这个学生，不新建
                    print("修改成功")
                else:
                    print("成绩不符合规范，不修改")
                return                                # 找到并处理完就结束
        print("没有找到该学生")                        # 循环走完没找到才提示

    # 3. 删除学生成绩
    def delete_student(self):
        name = input("请输入要删除的学生姓名：")
        for s in self.student_list:
            if s.name == name:
                self.student_list.remove(s)
                print("学生信息删除成功")
                return
        print("未找到该学生")

    # 4. 查询指定学生成绩
    def query_student(self):
        name = input("请输入要查询的学生姓名：")
        for s in self.student_list:
            if s.name == name:
                print(f"查询的学生成绩为：{s}")
                return
        print("未找到该学生成绩")

    # 5. 显示所有学生成绩
    def show_student(self):
        if len(self.student_list) == 0:
            print("暂无学生成绩")
            return
        for s in self.student_list:
            print(s)                                  # 循环里不要 return

# 主菜单：把系统真正用起来
def main():
    system = EduSystem()
    while True:
        print("""
===== 教务系统 =====
1. 添加学生成绩
2. 修改学生成绩
3. 删除学生成绩
4. 查询指定学生
5. 显示所有学生
0. 退出
""")
        choice = input("请输入选项：")
        if choice == "1":
            system.add_student()
        elif choice == "2":
            system.update_student()
        elif choice == "3":
            system.delete_student()
        elif choice == "4":
            system.query_student()
        elif choice == "5":
            system.show_student()
        elif choice == "0":
            print("再见！")
            break
        else:
            print("输入有误，请重新选择")

if __name__ == "__main__":
    main()
