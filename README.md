<div id="top"></div>


<!-- PROJECT LOGO -->
<br />
<div align="center">
    <img src="images/logo.png" alt="Logo" width="550" height="380">
  <h2 align="center">Programming Widget Layout</h2>
  <h3 align="center">Use the gained knowledge to create forms</h3>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
        <li><a href="#Experimenting-with-QHBOXLayout">Experimenting with QHBOXLayout</a></li>
        <li><a href="#Nested-Layouts">Nested Layouts</a></li>
        <li><a href="#Bug-report-Form">Bug report Form</a></li>
        <li><a href="#Grid-Layout">Grid Layout</a></li>
  </ol>
</details>



### Experimenting-with-QHBOXLayout

Create a project called `hbox` with the following code:

```cpp
int main(int argc, char* argv[])
{
  QApplication app(argc, argv);

  QWidget* window = new QWidget();
  window->setWindowTitle("QHBoxLayout Test");

  window->show();

  return app.exec();
}
```
This will show an **empty** window. Your goal is to modify the code in order to display the following form:

<p align="center">
     <img src="images/hbox.png">
   </p> 
  
   > A QHBoxLayout example.
 
 .Header

```cpp
class dialoge1 : public QWidget
{
public:
    explicit dialoge1(QWidget *parent = nullptr);
protected:
    void createWidgets();
    void placeWidgets();
protected:
    QLabel *namelabel;
    QLineEdit *line;
    QPushButton *search;
    QHBoxLayout *hlayout;
};
```
 
 .cpp
 
 ```cpp
dialoge1::dialoge1(QWidget *parent) : QWidget(parent)
{
    createWidgets();
    placeWidgets();
}
void dialoge1::createWidgets()
{

    namelabel   = new QLabel("Name");
    line        = new QLineEdit();
    search      = new QPushButton("Search");
    hlayout     = new QHBoxLayout();

    setLayout(hlayout);
    setWindowTitle("QHBoxLayout Test");

 }
void dialoge1::placeWidgets()
{
    hlayout->addWidget(namelabel);
    hlayout->addWidget(line);
    hlayout->addWidget(search);
}
```

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- The PNG class -->
### Nested-Layouts

The goal of the exercice is learn to analyse the construction of a form and thencode it using **Netsted layouts**.

Here we show you a classic dialog from the book **GB** to search for a user.

 > You do not have to code any **functinality**, just the form of the dialog.
 
 <p align="center">
     <img src="images/nesting.png">
   </p> 
 
  >Nested Layout.
.Header
```cpp
class Dialog2 : public QWidget
{
public:
    explicit Dialog2(QWidget *parent = nullptr);
protected:
    void createWidgets();
    void placeWidgets();
protected:
    QLabel *namelabel;
    QLineEdit *line;
    QPushButton *search;
    QPushButton *close;
    QHBoxLayout *mainLayout;
    QVBoxLayout *rightLayout;
    QVBoxLayout *leftLayout;
    QHBoxLayout *topLeftLayout;
    QCheckBox *match;
    QCheckBox *backward;
};
```

.cpp
```cpp
Dialog2::Dialog2(QWidget *parent) : QWidget(parent)
{
    createWidgets();
    placeWidgets();
}
void Dialog2::createWidgets()
{
    //Labels
    namelabel = new QLabel("Name");
    //Lines
    line   = new QLineEdit();
    //Buttons
    search  = new QPushButton("Search");
    close   = new QPushButton("Close");
    //checkboxes
    match    = new QCheckBox("Match case");
    backward = new QCheckBox("Search backward");
    //Layouts
    mainLayout    = new QHBoxLayout();   
    topLeftLayout = new QHBoxLayout();
    rightLayout   = new QVBoxLayout(); 
    leftLayout    = new QVBoxLayout();
    setLayout(mainLayout);
    setWindowTitle("Nested Layout Test");
    resize(400,200);
 }
void Dialog2::placeWidgets()
{
    //Layouts structure
    mainLayout->addLayout(leftLayout);
    mainLayout->addLayout(rightLayout);
    leftLayout->addLayout(topLeftLayout);
    //objects
    rightLayout->addWidget(search);
    rightLayout->addWidget(close);
    
    topLeftLayout->addWidget(namelabel);
    topLeftLayout->addWidget(line);
    
    leftLayout->addWidget(match);
    leftLayout->addWidget(backward);
    
    topLeftLayout->addSpacerItem(new QSpacerItem(15,0,QSizePolicy::Fixed));
    
    rightLayout->addSpacerItem(new QSpacerItem(10,50,QSizePolicy::Fixed));
}
```
 - In order to add a layout to a main one, you’ll have to use

      addLayout(layout)

 - The **vertical space** ([Stretch](https://doc.qt.io/qt-5.15/qboxlayout.html#addStretch)) could be added by
 
     - `layout->addStretch(dimension)` 
     - `layout->addSpacer(SpaceItem) `  
     
 - the Widget with a empty checkable **square** is a [QCheckBox](https://doc.qt.io/qt-5/qcheckbox.html)

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- Inhertance diagram -->
## Bug-report-Form

This example is taken from [Qt Tutorial](https://doc.qt.io/archives/qq/qq25-formlayout.html). You task is to create the following form to report a problem.

   <p align="center">
     <img src="images/form_report.png">
   </p> 
   
   > Dialog to report a form. 

.Header
```cpp
class BugRepForm: public QWidget
{
public:
    explicit BugRepForm(QWidget *parent = nullptr);
protected:
    void makeConnexion();
    void createWidgets();
    void placeWidgets();
protected:
    //Layouts
    QVBoxLayout *mainlayout;
    QVBoxLayout *toplayout;
    
    QHBoxLayout *midlayout;
    QHBoxLayout *botlayout;
    QHBoxLayout *namelayout;
    QHBoxLayout *companylayout;
    QHBoxLayout *phonelayout;
    QHBoxLayout *emaillayout;
    QHBoxLayout *problemTlayout;
    QHBoxLayout *summinfolayout;
    QHBoxLayout *reprodlayout;
    QHBoxLayout *combblayout;
    QHBoxLayout *resetlayout;
    QHBoxLayout *subm_layout;
    QHBoxLayout *not_slayout;
    //Labels
    QLabel *name;
    QLabel *company;
    QLabel *phone;
    QLabel *email;
    QLabel *problemT;
    QLabel *summinfo;
    QLabel *reprod;
    //Lines
    QLineEdit  *nameL;
    QLineEdit  *companyL;
    QLineEdit  *phoneL;
    QLineEdit  *emailL;
    QLineEdit  *problemTL;
    QTextEdit  *summinfoL;
    //Buttons
    QPushButton  *reset;
    QPushButton  *DONOTsubmit;
    QPushButton  *subBugRep;
    //Combo_Box
    QComboBox  *combB;
};
```
.cpp
```cpp
BugRepForm::BugRepForm(QWidget *parent) : QWidget(parent)
{
    createWidgets();
    placeWidgets();
}
void BugRepForm::createWidgets()
{
    //Layouts
    mainlayout         = new QVBoxLayout();
    toplayout          = new QVBoxLayout();
    midlayout          = new QHBoxLayout();
    botlayout          = new QHBoxLayout();
    namelayout         = new QHBoxLayout();
    companylayout      = new QHBoxLayout();
    phonelayout        = new QHBoxLayout();
    emaillayout        = new QHBoxLayout();
    problemTlayout     = new QHBoxLayout();
    summinfolayout     = new QHBoxLayout();
    reprodlayout       = new QHBoxLayout();
    combblayout        = new QHBoxLayout();
    resetlayout        = new QHBoxLayout();
    subm_layout        = new QHBoxLayout();
    not_slayout        = new QHBoxLayout();
    //Labels
    name      = new QLabel("Name:");
    company   = new QLabel("Company:");
    phone     = new QLabel("Phone:");
    email     = new QLabel("Email:");
    problemT  = new QLabel("Problem Title:");
    summinfo  = new QLabel("Summary information:");
    reprod    = new QLabel("Reproducibility:");
    //Lines
    nameL      = new QLineEdit();
    companyL   = new QLineEdit();
    phoneL     = new QLineEdit();
    emailL     = new QLineEdit();
    problemTL  = new QLineEdit();
    summinfoL  = new QTextEdit();
    //Buttons
    reset        = new QPushButton("Reset");
    DONOTsubmit  = new QPushButton("Don't Submit");
    subBugRep    = new QPushButton("Submit Bug Report");
    //Combo_Box
    combB   = new QComboBox;
    combB->addItem("Always");
    combB->addItem("Somtimes");
    combB->addItem("Rarely");
    
    setLayout(mainlayout);
    setWindowTitle("Report Bug");
    resize(600,600);
 }
void BugRepForm::placeWidgets()
{
    //Layouts structure
    mainlayout->addLayout(toplayout);
    mainlayout->addLayout(midlayout);
    mainlayout->addLayout(botlayout);

    toplayout->addLayout(namelayout);
    toplayout->addLayout(companylayout);
    toplayout->addLayout(phonelayout);
    toplayout->addLayout(emaillayout);
    toplayout->addLayout(problemTlayout);
    toplayout->addLayout(summinfolayout);

    midlayout->addLayout(reprodlayout);
    midlayout->addLayout(combblayout);

    botlayout->addLayout(resetlayout);
    botlayout->addLayout(subm_layout);
    botlayout->addLayout(not_slayout);
    //objects
    namelayout->addWidget(name);
    namelayout->addWidget(nameL);

    companylayout->addWidget(company);
    companylayout->addWidget(companyL);

    phonelayout->addWidget(phone);
    phonelayout->addWidget(phoneL);

    emaillayout->addWidget(email);
    emaillayout->addWidget(emailL);

    problemTlayout->addWidget(problemT);
    problemTlayout->addWidget(problemTL);

    summinfolayout->addWidget(summinfo);
    summinfolayout->addWidget(summinfoL);

    reprodlayout->addWidget(reprod);
    combblayout->addWidget(combB,1);
    resetlayout->addWidget(reset);
    subm_layout->addWidget(subBugRep);
    not_slayout->addWidget(DONOTsubmit);
    //spacing settings
    namelayout->setSpacing(132);
    companylayout->setSpacing(104);
    phonelayout->setSpacing(129);
    emaillayout->setSpacing(135);
    problemTlayout->setSpacing(72);
    summinfolayout->setSpacing(5);
    midlayout->setSpacing(60);
    resetlayout->addSpacerItem(new QSpacerItem(50,80,QSizePolicy::Expanding));
}
```


<p align="right">(<a href="#top">back to top</a>)</p>


<!-- Image -->
## Grid-Layout

For our final exercice, we will visit an imporant layout that we missed in class.

   - Check and read the documentation for the [QGridLayout](https://doc.qt.io/qt-5.15/qgridlayout.html)
   - Once you’ve read it, try to construct the following calculator:
   
   <p align="center">
     <img src="images/keypad.png">
   </p>
   
> Calculator using the Grid Layout. 

   - The component showing the number is called a [LCDNumber](https://doc.qt.io/archives/qt-4.8/qlcdnumber.html)
   - You may assume that at max it can contains **6 digits**.
   - Call the method `setMinimumHeight` on you LCDNumber to set a minimu height of **80** pixels.

.Header
```cpp
class Calculator : public QWidget
{
public:
    explicit Calculator(QWidget *parent = nullptr);
protected:
    void makeConnexion();
    void createWidgets();
    void placeWidgets();
protected:
    //Layouts
    QGridLayout *mainGridlayout;
    //Buttons
    QVector<QPushButton*> calelements;
    QPushButton *element;
    //lcd
    QLCDNumber *lcdnum;
private:
    int k=0;
};
```
.cpp
```cpp
Calculator::Calculator(QWidget *parent) : QWidget(parent)
{
    createWidgets();
    placeWidgets();
}
void Calculator::createWidgets()
{
    //Buttons
    for (int i=9;i>0;i--)
    {
        element  = new QPushButton(QString::number(i));
        calelements.push_back(element);
    }
    //LCDnum
    lcdnum  = new QLCDNumber();
    mainGridlayout = new QGridLayout;

    setLayout(mainGridlayout);
    setWindowTitle("Numeric Keypad");
    resize(340,320);
 }
void Calculator::placeWidgets()
{
    //Objects
    lcdnum->setMinimumHeight(80);
    mainGridlayout->addWidget(lcdnum,0,0,1,3);
    for (int i=1;i<=3 ;i++)
    {
        for (int j=0;j<=2;j++)
        {
            mainGridlayout->addWidget(calelements[k],i,j);
                    k++;
        }
    }
    mainGridlayout->addWidget(new QPushButton("0"),4,0);
    mainGridlayout->addWidget(new QPushButton("enter"),4,1,1,2);
}
```

<p align="right">(<a href="#top">back to top</a>)</p>

Our Team - [AIT EL KADI Ilyas](https://github.com/IlyasKadi) - [AZIZ Oussama](https://github.com/ATAMAN0)

Project Link: [Widgets_and_Layouts](https://github.com/IlyasKadi/Widgets_and_Layouts)

Encadré par : [Mr.BELCAID-Anass](https://anassbelcaid.github.io)

<p align="right">(<a href="#top">back to top</a>)</p>
