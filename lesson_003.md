# Build the Login + Signup UI

Our goal is to understand a few of the basic tools we use to build mobile apps. 

**Widgets** - building blocks of flutter apps, they are akin to lego blocks in that they help construct something bigger by fitting well with each other

#### Key Terms

**Container** - A box container that houses content

**Column** - A box that aligns content vertically. Content flows from top to bottom

**Row** - A box that aligns content horizonatally. Content flows from left to right

**Center** - A box that centers content to the center of the device

**Text** - A box that contains text 

**Textfield** - A box that accepts text from the user like a sign-in form

**Partial** - Content that you link together from another source file

**Abstraction** - Breaking a big problem into smaller problems and bringing them together 


We are going to use this tools to build our first login UI


<img width="333" alt="Screenshot 2024-05-13 at 2 16 50 PM" src="https://github.com/Hgp-GeniusLabs/Curriculum/assets/31968175/e40414e1-8093-4563-8fc3-02feadc83e54">
<img width="320" alt="Screenshot 2024-05-13 at 2 17 09 PM" src="https://github.com/Hgp-GeniusLabs/Curriculum/assets/31968175/a8273baf-c473-4afa-bbfd-9e6415c0e635">


Activity: 

The result of our walkthrough lesson will be these above screenshots. 

1. We will first start of by talking about the basic structure of flutter applications
2. We will go into scaffolds and build widgets. How do they contribute to the screens we create?
3. And then we will slowly walkthrough the app build for each screen, making sure we go over those key terms mentioned above
4. Things to consider, why is hierarchy important when building flutter apps.
5. Which of the widgets are responsible for the flow of widgets?
6. What's the importance of a scaffold and why didn't we not add an App for Login and Signup Screens?


### Initialize the App

We want to make sure we are running a Material App, you can follow on how to initiate the app below: 

```dart

import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';
import 'package:instagram/screens/login_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: ScreenUtilInit(designSize: Size(375, 812), child: LoginScreen()),
    );
  }
}
```

This above code will give you an error because you do not yet have a LoginScreen page. We will go and add the content for the login screen below: 

This should include the Text input field, and buttons to submit the data. No databse yet to save the content. 



# Video 1

### Table of contents
1. Login Page
2. Sign Up Page



## Login Page

#### packagees

- ScreenUtil (https://pub.dev/packages/flutter_screenutil/install)
- Firefase Auth (https://pub.dev/packages/firebase_auth/install)

You need to add those two packages to your pubspec.yaml file below cupertino_icons: ^1.0.6

```dart

cupertino_icons: ^1.0.6
flutter_screenutil: ^5.9.1
firebase_auth: ^4.19.5

```

- Start by creating a Login Screen file (login_screen.dart)

- Import the packages needed. 

```dart

import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';
import 'package:your_application_name/firebase_service/firebase_auth.dart';

```

- Initialize the state of the application by typing St and then autocompleting StatefulWidget

```dart

class MyWidget extends StatefulWidget {
  const MyWidget({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return const Placeholder();
  }
}


```

You will get a default version of a statefulwidget class that you then need to update MyWidget into LoginScreen, everywhere you see it above. 

Result after updating the class name

```dart

class LoginScreen extends StatefulWidget {
  const LoginScreen({super.key});

  @override
  State<LoginScreen> createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  @override
  Widget build(BuildContext context) {
    return const Placeholder();
  }
}

```


Instead of returning a Placeholder class, we are going to return a Scaffold(), which is predetermined structure of a flutter app (with appbar, body, etc). 



```dart

class _LoginScreenState extends State<LoginScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold();
  }
}

```

We are going to then move on and add a safe area for the content and wrap it with a column so we can align our content of the login page vertically. 

We are also adding our local variables which will store the users email and password as they input the data. 

```dart

class _LoginScreen extends State<MyWidget> {

  // User data

  final email = TextEditingController();
  FocusNode email_F = FocusNode();

  final password = TextEditingController();
  FocusNode password_F = FocusNode();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          children: [
            // any content that we will have for this screen will go here. 
          ],
        ),
      ),
    );
  }
}

```


First we are going to add a sized box and center widget for the logo: 

```dart

class _LoginScreen extends State<MyWidget> {

  // User data

  final email = TextEditingController();
  FocusNode email_F = FocusNode();

  final password = TextEditingController();
  FocusNode password_F = FocusNode();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          children: [
            // any content that we will have for this screen will go here.
            SizedBox(
              width: 96.w,
              height: 100.h,
            ),
            Center(
              child: Image.asset("images/logo.jpg"),
            ),
            SizedBox(height: 120.h),
          ],
        ),
      ),
    );
  }
}

```


Next we are going to create a custom Textfield widget that will be responsible for interacting with the user to login. 

When you first enter the function, you should receive an error. 



```dart

class _LoginScreen extends State<MyWidget> {

  // User data

  final email = TextEditingController();
  FocusNode email_F = FocusNode();

  final password = TextEditingController();
  FocusNode password_F = FocusNode();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          children: [
            // any content that we will have for this screen will go here.
            SizedBox(
              width: 96.w,
              height: 100.h,
            ),
            Center(
              child: Image.asset("images/logo.jpg"),
            ),
            SizedBox(height: 120.h),
            Textfield(email, Icons.email, 'Email', email_F),
          ],
        ),
      ),
    );
  }
}

// We need to define and create the function below:



Widget Textfield(TextEditingController controller, IconData icon, String type,
      FocusNode focus) {
    return Container(
      child: Padding(
        padding: EdgeInsets.symmetric(horizontal: 10.w),
        child: TextField(
          style: TextStyle(fontSize: 18.sp, color: Colors.black),
          controller: controller,
          focusNode: focus,
          decoration: InputDecoration(
              hintText: type,
              prefixIcon: Icon(icon,
                  color: focus.hasFocus ? Colors.black : Colors.grey),
              contentPadding:
                  EdgeInsets.symmetric(horizontal: 15.w, vertical: 15.h),
              enabledBorder: OutlineInputBorder(
                borderRadius: BorderRadius.circular(5.r),
                borderSide: BorderSide(
                  color: Colors.grey,
                  width: 2.w,
                ),
              ),
              focusedBorder: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(5.r),
                  borderSide: BorderSide(
                    color: Colors.black,
                    width: 2.w,
                  ))),
        ),
      ),
    );
  }


```


Next we need to add the forget button. I'm going to only grab the buildwidget in here so we don't copy over and over again. 



```dart 
Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          children: [
            // any content that we will have for this screen will go here.
            SizedBox(
              width: 96.w,
              height: 100.h,
            ),
            Center(
              child: Image.asset("images/logo.jpg"),
            ),
            SizedBox(height: 120.h),
            Textfield(email, Icons.email, 'Email', email_F),

            // new

            forget(),
            SizedBox(height: 15.h),
          ],
        ),
      ),
    );

....


// we need to define the function in the same way below:

Padding forget() {
    return Padding(
      padding: EdgeInsets.only(left: 230.w),
      child: GestureDetector(
        onTap: () {},
        child: Text(
          'Forgot password?',
          style: TextStyle(
            fontSize: 13.sp,
            color: Colors.blue,
            fontWeight: FontWeight.w500,
          ),
        ),
      ),
    );
  }

....

``` 

Next we need to add the login and signup leading buttons to finish the login page. 



```dart
Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          children: [
            // any content that we will have for this screen will go here.
            SizedBox(
              width: 96.w,
              height: 100.h,
            ),
            Center(
              child: Image.asset("images/logo.jpg"),
            ),
            SizedBox(height: 120.h),
            Textfield(email, Icons.email, 'Email', email_F),
            forget(),
            SizedBox(height: 15.h),

            // new

            login(),
            SizedBox(height: 15.h),
            Have()
          ],
        ),
      ),
    );

....

// below we need to define both widget functions:

Widget login() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Container(
        alignment: Alignment.center,
        width: double.infinity,
        height: 44.h,
        decoration: BoxDecoration(
          color: Colors.black,
          borderRadius: BorderRadius.circular(10.r),
        ),
        child: Text(
          'Login',
          style: TextStyle(
            fontSize: 23.sp,
            color: Colors.white,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }


  ....


  Widget Have() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          Text(
            "Don't have account?  ",
            style: TextStyle(
              fontSize: 14.sp,
              color: Colors.grey,
            ),
          ),
          GestureDetector(
            onTap: widget.show,
            child: Text(
              "Sign Up",
              style: TextStyle(
                  fontSize: 15.sp,
                  color: Colors.blue,
                  fontWeight: FontWeight.bold),
            ),
          ),
        ],
      ),
    );
  }

```

That completes our login screen flutter page. 

After everything is compliled and put together, you should have the following code below: 


```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

class LoginScreen extends StatefulWidget {

  // we will explain this later down
  final VoidCallback show;
  const LoginScreen(this.show,{super.key});

  @override
  State<LoginScreen> createState() => _LoginScreenState();
}

class _LoginScreenState extends State<LoginScreen> {
  final email = TextEditingController();
  FocusNode email_F = FocusNode();

  final password = TextEditingController();
  FocusNode password_F = FocusNode();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      body: SafeArea(
        child: Column(
          children: [
            SizedBox(
              width: 96.w,
              height: 100.h,
            ),
            Center(
              child: Image.asset("images/logo.jpg"),
            ),
            SizedBox(height: 120.h),
            Textfield(email, Icons.email, 'Email', email_F),
            SizedBox(height: 15.h),
            Textfield(password, Icons.lock, 'Password', password_F),
            forget(),
            SizedBox(height: 15.h),
            login(),
            SizedBox(height: 15.h),
            Have()
          ],
        ),
      ),
    );
  }

  Widget Textfield(TextEditingController controller, IconData icon, String type,
      FocusNode focus) {
    return Container(
      child: Padding(
        padding: EdgeInsets.symmetric(horizontal: 10.w),
        child: TextField(
          style: TextStyle(fontSize: 18.sp, color: Colors.black),
          controller: controller,
          focusNode: focus,
          decoration: InputDecoration(
              hintText: type,
              prefixIcon: Icon(icon,
                  color: focus.hasFocus ? Colors.black : Colors.grey),
              contentPadding:
                  EdgeInsets.symmetric(horizontal: 15.w, vertical: 15.h),
              enabledBorder: OutlineInputBorder(
                borderRadius: BorderRadius.circular(5.r),
                borderSide: BorderSide(
                  color: Colors.grey,
                  width: 2.w,
                ),
              ),
              focusedBorder: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(5.r),
                  borderSide: BorderSide(
                    color: Colors.black,
                    width: 2.w,
                  ))),
        ),
      ),
    );
  }

  Padding forget() {
    return Padding(
      padding: EdgeInsets.only(left: 230.w),
      child: GestureDetector(
        onTap: () {},
        child: Text(
          'Forgot password?',
          style: TextStyle(
            fontSize: 13.sp,
            color: Colors.blue,
            fontWeight: FontWeight.w500,
          ),
        ),
      ),
    );
  }


  Widget login() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Container(
        alignment: Alignment.center,
        width: double.infinity,
        height: 44.h,
        decoration: BoxDecoration(
          color: Colors.black,
          borderRadius: BorderRadius.circular(10.r),
        ),
        child: Text(
          'Login',
          style: TextStyle(
            fontSize: 23.sp,
            color: Colors.white,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }

  Widget Have() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          Text(
            "Don't have account?  ",
            style: TextStyle(
              fontSize: 14.sp,
              color: Colors.grey,
            ),
          ),
          GestureDetector(
            onTap: widget.show,
            child: Text(
              "Sign Up",
              style: TextStyle(
                  fontSize: 15.sp,
                  color: Colors.blue,
                  fontWeight: FontWeight.bold),
            ),
          ),
        ],
      ),
    );
  }

}
```


## Toggle Between login and signup 

We want to be able to switch back and forth when we first launch the app. 

If we want to login, then we continue because that's the default page, if not, then we wanna press to register a new user. 

This AuthScreen class will help us flip back and forth. 

```dart

import 'package:flutter/material.dart';
import 'package:flutter_instagram_clone/screen/login_screen.dart';
import 'package:flutter_instagram_clone/screen/signup.dart';

class AuthScreen extends StatefulWidget {
  const AuthScreen({super.key});

  @override
  State<AuthScreen> createState() => _AuthScreenState();
}

class _AuthScreenState extends State<AuthScreen> {
  bool a = true;
  void go() {
    setState(() {
      a = !a;
    });
  }

  @override
  Widget build(BuildContext context) {
    if (a) {
      return LoginScreen(go);
    } else {
      return SignupScreen(go);
    }
  }
}
```


# Signup Screen 

The signup page is very similar to the login, except you have two more text fields and an updated avatar widget to accept a user profile picture. 

Code is below. 


```dart

import 'dart:io';

import 'package:flutter/material.dart';
import 'package:flutter_instagram_clone/data/firebase_service/firebase_auth.dart';
import 'package:flutter_instagram_clone/util/dialog.dart';
import 'package:flutter_instagram_clone/util/exeption.dart';
import 'package:flutter_instagram_clone/util/imagepicker.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

class SignupScreen extends StatefulWidget {
  final VoidCallback show;
  SignupScreen(this.show, {super.key});

  @override
  State<SignupScreen> createState() => _SignupScreenState();
}

class _SignupScreenState extends State<SignupScreen> {
  final email = TextEditingController();
  FocusNode email_F = FocusNode();
  final password = TextEditingController();
  FocusNode password_F = FocusNode();
  final passwordConfirme = TextEditingController();
  FocusNode passwordConfirme_F = FocusNode();
  final username = TextEditingController();
  FocusNode username_F = FocusNode();
  final bio = TextEditingController();
  FocusNode bio_F = FocusNode();
  File? _imageFile;
  @override
  void dispose() {
    // TODO: implement dispose
    super.dispose();
    email.dispose();
    password.dispose();
    passwordConfirme.dispose();
    username.dispose();
    bio.dispose();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomInset: false,
      backgroundColor: Colors.white,
      body: SafeArea(
        child: Column(
          children: [
            SizedBox(width: 96.w, height: 10.h),
            Center(
              child: Image.asset('images/logo.jpg'),
            ),
            SizedBox(width: 96.w, height: 70.h),
            InkWell(
              onTap: () async {
                File _imagefilee = await ImagePickerr().uploadImage('gallery');
                setState(() {
                  _imageFile = _imagefilee;
                });
              },
              child: CircleAvatar(
                radius: 36.r,
                backgroundColor: Colors.grey,
                child: _imageFile == null
                    ? CircleAvatar(
                        radius: 34.r,
                        backgroundImage: AssetImage('images/person.png'),
                        backgroundColor: Colors.grey.shade200,
                      )
                    : CircleAvatar(
                        radius: 34.r,
                        backgroundImage: Image.file(
                          _imageFile!,
                          fit: BoxFit.cover,
                        ).image,
                        backgroundColor: Colors.grey.shade200,
                      ),
              ),
            ),
            SizedBox(height: 40.h),
            Textfild(email, email_F, 'Email', Icons.email),
            SizedBox(height: 15.h),
            Textfild(username, username_F, 'username', Icons.person),
            SizedBox(height: 15.h),
            Textfild(bio, bio_F, 'bio', Icons.abc),
            SizedBox(height: 15.h),
            Textfild(password, password_F, 'Password', Icons.lock),
            SizedBox(height: 15.h),
            Textfild(passwordConfirme, passwordConfirme_F, 'PasswordConfirme',
                Icons.lock),
            SizedBox(height: 15.h),
            Signup(),
            SizedBox(height: 15.h),
            Have()
          ],
        ),
      ),
    );
  }

  Widget Have() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          Text(
            "Don you have account?  ",
            style: TextStyle(
              fontSize: 14.sp,
              color: Colors.grey,
            ),
          ),
          GestureDetector(
            onTap: widget.show,
            child: Text(
              "Login ",
              style: TextStyle(
                  fontSize: 15.sp,
                  color: Colors.blue,
                  fontWeight: FontWeight.bold),
            ),
          ),
        ],
      ),
    );
  }

  Widget Signup() {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: InkWell(
        onTap: () async {
          try {
            await Authentication().Signup(
              email: email.text,
              password: password.text,
              passwordConfirme: passwordConfirme.text,
              username: username.text,
              bio: bio.text,
              profile: _imageFile ?? File(''),
            );
          } on exceptions catch (e) {
            dialogBuilder(context, e.message);
          }
        },
        child: Container(
          alignment: Alignment.center,
          width: double.infinity,
          height: 44.h,
          decoration: BoxDecoration(
            color: Colors.black,
            borderRadius: BorderRadius.circular(10.r),
          ),
          child: Text(
            'Sign up',
            style: TextStyle(
              fontSize: 23.sp,
              color: Colors.white,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ),
    );
  }

  Padding Textfild(TextEditingController controll, FocusNode focusNode,
      String typename, IconData icon) {
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: 10.w),
      child: Container(
        height: 44.h,
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.circular(5.r),
        ),
        child: TextField(
          style: TextStyle(fontSize: 18.sp, color: Colors.black),
          controller: controll,
          focusNode: focusNode,
          decoration: InputDecoration(
            hintText: typename,
            prefixIcon: Icon(
              icon,
              color: focusNode.hasFocus ? Colors.black : Colors.grey[600],
            ),
            contentPadding:
                EdgeInsets.symmetric(horizontal: 15.w, vertical: 15.h),
            enabledBorder: OutlineInputBorder(
              borderRadius: BorderRadius.circular(5.r),
              borderSide: BorderSide(
                width: 2.w,
                color: Colors.grey,
              ),
            ),
            focusedBorder: OutlineInputBorder(
              borderRadius: BorderRadius.circular(5.r),
              borderSide: BorderSide(
                width: 2.w,
                color: Colors.black,
              ),
            ),
          ),
        ),
      ),
    );
  }
}

```

























