Title: Django database modelling
Date: 2011-01-04 10:20
Category: django
Tags: django, db, python
Slug: django-db-modelling
Author: Shabda Raaj
Summary: How to design DBs with django models.

Django abstracts most of the actions you would be doing with the Database.
What it doesn't abstracts, and doesn't try to abstract is the Database modelling part. This is a quick tutorial
describing to how model your data in Django models.py, and how to access and modify them.

Consider a hypothetical HR department, which wants you to build an application to track and manage their processes.
They have employees who work for a department, contractors who work for multiple department. Let's see how you
you would do that in Django.


    from django.db import models

    class Employee(models.Model):
        name = models.CharField(max_length = 100)
        department = models.ForeignKey("Department")

    class Department(models.Model):
        name = models.CharField(max_length = 100)

    class EmployeeHistory(models.Model):
        employee = models.OneToOneField(Employee)
        date_joined = models.DateField()
        marital_status = models.BooleanField()

    class Contactor(models.Model):
        name = models.CharField(max_length = 100)
        departments = models.ManyToManyField(Department)


Let's see the type of relationship we created here.

An `Employee` has a Many-to-one relationship with `Department`, (i.e. One department will have many
`Employee`, but one employee will have a single departments.)

So `Employee` has a field `department = models.ForeignKey("Department")`. See that the `ForeignKey` field
was added on the class which has in *many*. In database, this creates a FK from in `Employee` table which refernces
`Departments`.

A `Contractor` has mant-to-many relationships with `Department`, so it has a `ManyToMany` field. This field can be created
on either classes. At a database level this creates a new table which has a FK to both the tables.

A `Employee` has one-to-one relationship with `EmployeeHistory`. The thing to note here is that whatever we could do with
OneToOneField, we can do by including the fields in the Other Class directly. However when there are fields which are only rarely
needed with a given model, it is useful to separate them via a one-to-one field. The one to one field can be on either class.


#### Accessing objects.

##### Getting a specific employee.

    Employee.objects.get(pk = someval)
    Employee.objects.get(name= someval)

##### Given an department get all employees.

    department.employee_set.all()

The `department` gets an attribute name `<FKClass>_set`.

Given an employee, get all colleagues.

    employee.department.employee_set.objects.all()

To get siblings, get parents, and get all children.

Given an department, get number of employees.

    department.employee_set.all().count()


Ok so the HR department bosses are happy with what they see, and ask you to track this data,
who is the manager of each employee, who is the HOD of each department and when did each employee took leave.


    from django.db import models

    class Employee(models.Model):
        name = models.CharField(max_length = 100)
        manager = models.ForeignKey("self", blank = True, null = True)
        department = models.ForeignKey("Department")

    class Department(models.Model):
        hod = models.ForeignKey("Employee")
        name = models.CharField(max_length = 100)

    class EmployeeHistory(models.Model):
        employee = models.OneToOneField(Employee)
        date_joined = models.DateField()
        marital_status = models.BooleanField()

    class Contactors(models.Model):
        name = models.CharField(max_length = 100)
        departments = models.ManyToManyField(Department)


    class EmployeeLeave(models.Model):
        leave_taken = models.DateField()
        employee = models.ForeignKey(Employee)

So we now have new fields `hod = models.OneToOneField("Employee")` in department and
`manager = models.ForeignKey("self", blank = True, null = True)` and a new model `EmployeeLeave`. Let su see
the new realtions,

As one `Department` will have one `Employee` as hod, and `Employee` can head at max one `Department`, we have a one to one relationship
As many `Employee` will report to another `Employee`, so we have a FK on `Employee`, referencing `self`.
As `Employee` will take many `EmployeeLeave`, `EmployeeLeave` has a FK to `Epployee`

Let us see some queries.


Get all leaves taken by an employee this year

    import datetime
    today = datetime.date.today()
    start_of_year = datetime.datetime(today.year, 1, 1)
    leaves_taken = employee.employeeleave_set.filter(leave_taken__gt=start_of_year, leave_taken__lt = today)


Get a list of all HODs.

    #As there are going to be as many Employees as departments
    departments = Department.objects.all()
    employees = [department.hod for department in departments]

Get a list of all departments a contractor works for.

    contractor.department_set.all()

Get a list of all contractor who work for a department.

    department.contractor_set.all()

Note that each side of a many to many relationship get a Manager.

List of all managers in a given department.

    Todo

List of all leaves taken in a given department.

    EmployeeLeave.objects.filter(employee__department = department)

None that we used double underscores `__` to do a filtering on a field across Entities.

List of all employees which joined a given department this year.

    Employee.objects.filter(department = department, employment_history__date_joined__gte=start_of_year, )

Note that we used a double underscore `__` twice, first to go across entities, and then to define the type of filter(`__gte`).
Also we specified two filter conditions, so they were `ANDed` together.

List all employees which either report too a given employee, or joined before him.

    Employee.objects.filter(Q(manager = employee)|Q(employee_history__date_joined__lt = employee.employee_history.date_joined))

Note the new construct `Q`, they are used to specify complex boolean operations. Here we used the `|` (or operator) to specify or condition.

-----

[Do you subscribe to our rss feed](http://feeds.feedburner.com/uswarearticles)? The new feed has full text feed and many other goodness. So make sure you are subscribed to the new feed with extra fortified vitamins. [Subscribe now](http://feeds.feedburner.com/uswarearticles).


