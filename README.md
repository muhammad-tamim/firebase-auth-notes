<h1 align="center">Firebase Authentication</h1>

- [Setup firebase:](#setup-firebase)
- [SingUp with email \& password and signIn, signOut:](#singup-with-email--password-and-signin-signout)
- [SignIn and signOut with google:](#signin-and-signout-with-google)
- [SignIn and SignOut with GitHub:](#signin-and-signout-with-github)
- [SignIn and SignOut with Facebook:](#signin-and-signout-with-facebook)
- [SignIn and SignOut with Twitter:](#signin-and-signout-with-twitter)
- [Manage Users:](#manage-users)
    - [Get Current signin user info:](#get-current-signin-user-info)
      - [Using onAuthStateChanged (recommended):](#using-onauthstatechanged-recommended)
      - [Using auth.currentUser:](#using-authcurrentuser)
    - [using Using the Returned userCredential](#using-using-the-returned-usercredential)
    - [Update Profile:](#update-profile)
    - [Send a user verification email \& password reset email](#send-a-user-verification-email--password-reset-email)
    - [Delete a user:](#delete-a-user)
- [example:](#example)
    - [Example 1:](#example-1)


# Setup firebase: 
- step 1: First install the firebase, then Go to the firebase console and create a project and follow the auth docs: 

```jsx
npm install firebase
```

https://console.firebase.google.com/

https://firebase.google.com/docs/auth

- step 2: 

```jsx
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

const firebaseConfig = {
  apiKey: "AIza...............................",
  authDomain: "module-49......................",
  projectId: "module-49.......................",
  storageBucket: "module-49...................",
  messagingSenderId: "........................",
  appId: "1:422912............................."
};

const app = initializeApp(firebaseConfig);

export const auth = getAuth(app);
```

# SingUp with email & password and signIn, signOut:

- Step 1: 

Go to the firebase console / build / Authentication and set methods: 

![image](/images/sing-in-methods.png)

- step 2: SignUp

```jsx
import { createUserWithEmailAndPassword } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

createUserWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    console.log(userCredential)
  })
  .catch((error) => {
    console.log(error)
  });
```

- step 3: SignIn

```jsx
import { signInWithEmailAndPassword } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    console.log(userCredential)
  })
  .catch((error) => {
    console.log(error)
  });
```

- step 4: SignOut

```jsx
import { signOut } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signOut(auth)
    .then(() => {
    })
    .catch((error) => {
        console.log(error)
    });
```

# SignIn and signOut with google: 

- step 1: 

Go to the firebase console / build / Authentication and set Sign-in methods: 

![image](/images/sing-in-methods.png)


- step 2: SignIn

```jsx
import { signInWithPopup, GoogleAuthProvider } from "firebase/auth";
import { auth } from '../firebase/firebase.init';


const provider = new GoogleAuthProvider();

signInWithPopup(auth, provider)
    .then((result) => {
        console.log(result)
    })
    .catch((error) => {
        console.log(error)
    });
```

- step 3: SignOut

```jsx
import { signOut } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signOut(auth)
    .then(() => {
    })
    .catch((error) => {
        console.log(error)
    });
```

# SignIn and SignOut with GitHub:

- step 1: 

Go to the firebase console / build / Authentication and set Sign-in methods: 

![image](/images/sing-in-methods.png)

now, if you want to select github you will see this fields: 

![image](/images/github-form.png)

- step 2: 

go to the github: settings/Developer Settings / create new Github App / and fell the form:

![image](/images/create-githu-app-form.png)

after completing the form will give see client id and secret like this, so use this to your firebase github methods form: 

![image](/images/github-clientid-and-secreat.png)

![image](/images/firebase-github-fell-form.png)

- step 3: signIn

```jsx
import { GithubAuthProvider, signInWithPopup } from 'firebase/auth';
import { auth } from '../firebase/firebase.init';

const provider = new GithubAuthProvider();

signInWithPopup(auth, provider)
    .then((result) => {
        console.log(result)
    })
    .catch((error) => {
        console.log(error)
    });
```

- step 4: signOut

```jsx
import { signOut } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signOut(auth)
    .then(() => {
    })
    .catch((error) => {
        console.log(error)
    });
```

# SignIn and SignOut with Facebook:

- step 1: Firebase

Go to the firebase console / build / Authentication and set Sign-in methods: 

![image](/images/sing-in-methods.png)

now, if you want to select facebook you will see this fields: 

![image](/images/firebase-appid-appsecret.png)

- step 2: Facebook

go to the and you will see getStarted button on the right side of the page, click that button. if you are new it will redirect you to register page but if you already register it will show you to the create apps page, where you can create apps.

https://developers.facebook.com

https://developers.facebook.com/apps/

![image](/images/get-started.png)

![image](/images/app.png)

if you press the create apps button it will show you couple of forms, just fill the forms. after that you will find dashboard page. in the dashboard page, you will see app Setting/basic, click it: 

![image](/images/dashboard.png)

here, you will find you AppId and App Secret that need on the firebase: 

![image](/images/facebookAppSecret.png)


- step 3: signIn

```jsx
import {signInWithPopup, FacebookAuthProvider } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

const provider = new FacebookAuthProvider();

signInWithPopup(auth, provider)
  .then((result) => {

    // This gives you a Facebook Access Token. You can use it to access the Facebook API.
    const credential = FacebookAuthProvider.credentialFromResult(result);
    const accessToken = credential.accessToken;

    console.log(result)
    console.log(accessToken)
  })
  .catch((error) => {
    console.log(error)
  });
```

- step 4: signOut

```jsx
import { signOut } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signOut(auth)
    .then(() => {
    })
    .catch((error) => {
        console.log(error)
    });
```

# SignIn and SignOut with Twitter:

- step 1: Firebase

Go to the firebase console / build / Authentication and set Sign-in methods: 

![image](/images/sing-in-methods.png)

now, if you want to select twitter you will see this fields: 

![image](/images/twitter-firebse.png)

- step 2: twitter

go to the https://developer.x.com/en and then press developer portal on the right side in the navbar, then it redirects you to this page https://developer.x.com/en/portal/dashboard. Then in the dashboard you find api key and secret: 

![image](/images/twitter-keyandtoken.png)


- step 3: signIn

```jsx
import {signInWithPopup, TwitterAuthProvider } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

const provider = new FacebookAuthProvider();

signInWithPopup(auth, provider)
  .then((result) => {
    const credential = TwitterAuthProvider.credentialFromResult(result);
    const token = credential.accessToken;
    const secret = credential.secret;
    
  }).catch((error) => {
    console.log(error)
  });
```

- step 4: signOut

```jsx
import { signOut } from "firebase/auth";
import { auth } from '../firebase/firebase.init';

signOut(auth)
    .then(() => {
    })
    .catch((error) => {
        console.log(error)
    });
```

# Manage Users: 

### Get Current signin user info:

#### Using onAuthStateChanged (recommended):

```jsx
import {onAuthStateChanged } from "firebase/auth";
import { auth } from "../firebase/firebase.init";

onAuthStateChanged(auth, (user) => {
    if (user) {
        console.log(user)
    } else {
        console.log("not found")
    }
});
```

#### Using auth.currentUser: 

```jsx
import { getAuth } from "firebase/auth";

const auth = getAuth();
const user = auth.currentUser;

if (user !== null) {
  console.log(user)
} else {
  console.log("no user")
}
```

note: auth.currentUser might return null immediately after page load because Firebase takes a moment to restore the user's session from storage.


### using Using the Returned userCredential

When you call Firebase methods like:
- createUserWithEmailAndPassword()
- signInWithEmailAndPassword()
- signInWithPopup()

They all return a Promise that resolves to a userCredential object.
You can access the current user instantly from it, right after successful authentication.

```jsx
import { createUserWithEmailAndPassword } from "firebase/auth";
import { auth } from "../firebase/firebase.init";

createUserWithEmailAndPassword(auth, email, password)
    .then((userCredential) => {
        // userCredential contains the user info
        const user = userCredential.user;
        console.log("User created and signed in:", user);
    })
    .catch((error) => {
        console.error("Signup error:", error);
    });
```

Note: 
- onAuthStateChanged() - Always running listener - Best for tracking user state across your entire app.
- auth.currentUser - Quick check - Access user info if Firebase is already initialized.
- userCredential.user - Immediately after sign-up/sign-in - Get the current user instantly after authentication actions.

### Update Profile: 

```jsx
import { getAuth, updateProfile } from "firebase/auth";

const auth = getAuth();

updateProfile(auth.currentUser, {
  displayName: "Jane Q. User", photoURL: "https://example.com/jane-q-user/profile.jpg"
}).then(() => {
  console.log("Profile Updated")
}).catch((error) => {
  console.log(error)
});
```

You can also set a user's email address with the updateEmail and user password updatePassword methods:

```jsx
import { getAuth, updateEmail } from "firebase/auth";
const auth = getAuth();
updateEmail(auth.currentUser, "user@example.com").then(() => {
  console.log("email updated successful")
}).catch((error) => {
  console.log(error)
});
```

```jsx
import { getAuth, updatePassword } from "firebase/auth";

const auth = getAuth();

const user = auth.currentUser;
const newPassword = "getASecureRandomPassword";

updatePassword(user, newPassword).then(() => {
  console.log("Update successful")
}).catch((error) => {
  console.log(error)
});
```

### Send a user verification email & password reset email

```jsx
import { getAuth, sendEmailVerification } from "firebase/auth";

const auth = getAuth();

sendEmailVerification(auth.currentUser)
  .then(() => {
    console.log("verification mail sent")
  });
```

```jsx
import { getAuth, sendPasswordResetEmail } from "firebase/auth";

const auth = getAuth();
sendPasswordResetEmail(auth, email)
  .then(() => {
    console.log("Password reset email sent!")
  })
  .catch((error) => {
    console.log(error)
  });
```

### Delete a user:

```jsx
import { getAuth, deleteUser } from "firebase/auth";

const auth = getAuth();
const user = auth.currentUser;

deleteUser(user).then(() => {
  console.log("User deleted")
}).catch((error) => {
  console.log(error)
});
```


# example: 

### Example 1:

```jsx
// AuthContext.jsx
import { createContext } from "react";

export const AuthContext = createContext(null)
```

```jsx
// AuthProvider.jsx
import React, { useEffect, useState } from 'react';
import { AuthContext } from '../contexts/AuthContext';
import { createUserWithEmailAndPassword, getAuth, GithubAuthProvider, GoogleAuthProvider, onAuthStateChanged, signInWithEmailAndPassword, signInWithPopup, signOut, updateProfile } from 'firebase/auth';
import { app } from '../firebase/firebase.config';

const AuthProvider = ({ children }) => {

    const auth = getAuth(app)

    const googleProvider = new GoogleAuthProvider()
    const githubProvider = new GithubAuthProvider()

    const [user, setUser] = useState(null)
    const [loading, setLoading] = useState(true)


    const signUpUser = (email, password) => {
        setLoading(true)
        return createUserWithEmailAndPassword(auth, email, password);
    }

    const signInUser = (email, password) => {
        setLoading(true)
        return signInWithEmailAndPassword(auth, email, password);
    }

    const signInUserWithGoogle = () => {
        setLoading(true)
        return signInWithPopup(auth, googleProvider)
    }

    const signInUserWithGithub = () => {
        setLoading(true)
        return signInWithPopup(auth, githubProvider)
    }

    const signOutUser = () => {
        setLoading(true)
        return signOut(auth);
    }

    const updateUserInfo = (updatedData) => {
        return updateProfile(auth.currentUser, updatedData);
    }

    // get current user
    useEffect(() => {
        const unSubscribe = onAuthStateChanged(auth, (currentUser) => {
            setUser(currentUser)
            setLoading(false)
        })
        return () => {
            unSubscribe()
        }
    }, [auth])

    const userInfo = {
        user,
        setUser,
        loading,
        signUpUser,
        signInUser,
        signInUserWithGoogle,
        signInUserWithGithub,
        signOutUser,
        updateUserInfo
    }

    return (
        <AuthContext value={userInfo}>
            {children}
        </AuthContext>
    );
};

export default AuthProvider;
```

```jsx
// main.jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client';
import './index.css'
import { RouterProvider } from 'react-router';
import { router } from './routes/Router';
import AuthProvider from './providers/AuthProvider';


createRoot(document.getElementById('root')).render(
  <StrictMode>
    <AuthProvider>
      <RouterProvider router={router}></RouterProvider>
    </AuthProvider>
  </StrictMode>,
)
```

```jsx
// PrivateRoute.jsx
import React, { use } from 'react';
import { AuthContext } from '../context/AuthContext';
import { Navigate, useLocation } from 'react-router';
import LoadingSpinner from '../components/LoadingSpinner';

const PrivateRoute = ({ children }) => {
    const location = useLocation();
    console.log(location)
    const { user, loading } = use(AuthContext)

    if (loading) {
        return <LoadingSpinner></LoadingSpinner>
    }

    if (!user) {
        return <Navigate to="/sign-in" state={location.pathname}></Navigate>
    }

    return children
};

export default PrivateRoute;
```

```jsx
// router.jsx
import { createBrowserRouter } from "react-router";
import MainLayout from "../layouts/MainLayout";
import HomePage from "../pages/HomePage";
import SignIn from "../pages/SignIn";
import SignUp from "../pages/SignUp";
import Orders from "../pages/Orders";
import Profile from "../pages/Profile";
import PrivateRoute from "./PrivateRoute";
import Dashboard from "../pages/Dashboard";

export const router = createBrowserRouter([
    {
        path: '/',
        element: <MainLayout></MainLayout>,
        children: [
            {
                index: true,
                element: <HomePage></HomePage>
            },
            {
                path: 'sign-in',
                element: <SignIn></SignIn>
            },
            {
                path: 'sign-up',
                element: <SignUp></SignUp>
            },
            {
                path: 'orders',
                element: (
                    <PrivateRoute>
                        <Orders></Orders>
                    </PrivateRoute>
                )
            },
            {
                path: 'profile',
                element: <PrivateRoute>
                    <Profile></Profile>
                </PrivateRoute>
            },
            {
                path: 'dashboard',
                element: <PrivateRoute>
                    <Dashboard></Dashboard>
                </PrivateRoute>
            }
        ]
    },
]);
```

```jsx
// SignIn.jsx
import React, { use } from 'react';
import { Link, useLocation, useNavigate } from 'react-router';
import { AuthContext } from '../context/AuthContext';
import { FaGoogle, FaGithub } from 'react-icons/fa';

const SignIn = () => {
    const { signInUser, signInUserWithGoogle, signInUserWithGithub } = use(AuthContext)
    const navigate = useNavigate();
    const location = useLocation()

    const handleSignIn = (e) => {
        e.preventDefault()

        const email = e.target.email.value
        const password = e.target.password.value

        signInUser(email, password)
            .then(() => {
              console.log('Login Successful')
                navigate(location?.state || '/')
            })
            .catch((error) => {
                console.log(error)
            });
    }


    const handleGoogleClick = () => {
        signInUserWithGoogle()
            .then(() => {
                console.log('Login Successful')
                navigate(location?.state || '/')
            })
            .catch((error) => {
                console.log(error)
            });
    }

    const handleGithubClick = () => {
        signInUserWithGithub()
            .then(() => {
                console.log('Login Successful')
                navigate(location?.state || '/')
            })
            .catch((error) => {
                console.log(error)
            });
    }

    return (
        <div className='min-h-[calc(100vh-148px)] flex flex-col gap-5 items-center justify-center bg-gray-300'>
            <h1>SignIn</h1>
            <form onSubmit={handleSignIn} className='flex flex-col gap-5'>
                <input type="email" name='email' className='input' placeholder='email' />
                <input type="password" name='password' className='input' placeholder='password' />
                <button className='btn' type='submit'>SignIn</button>
                <p>Don't have an account, <Link to={"sign-up"} className='text-blue-500'>SignUp</Link></p>
                <hr />
                <button onClick={handleGoogleClick} className='btn btn-circle mx-auto'><FaGoogle></FaGoogle></button>
                <button onClick={handleGithubClick} className='btn btn-circle mx-auto'><FaGithub></FaGithub></button>
            </form>
        </div >
    );
};

export default SignIn;
```

```jsx
// SignUp.jsx
import React, { use } from 'react';
import { Link, useNavigate } from 'react-router';
import { AuthContext } from '../context/AuthContext';
import { FaGoogle, FaGithub } from 'react-icons/fa';

const SignUp = () => {
    const navigate = useNavigate();
    const { signUpUser, signInUserWithGoogle, signInUserWithGithub, setUser, UpdateUserInfo } = use(AuthContext)

const handleSignUp = (e) => {
        e.preventDefault()

        const name = e.target.name.value
        const url = e.target.url.value
        const email = e.target.email.value
        const password = e.target.password.value

        signUpUser(email, password)
            .then((result) => {
                console.log('Sign Up Successful')
                const user = result.user

                updateUserInfo({ displayName: name, photoURL: url })
                    .then(() => {
                        setUser({ ...user, displayName: name, photoURL: url })
                        navigate('/news/1')
                    })
                    .catch(() => {
                        setUser(user)
                    })

            })
            .catch((error) => {
                console.log(error)
            })
    }


    const handleGoogleClick = () => {
        signInUserWithGoogle()
            .then(() => {
                console.log('Login Successful')
                navigate('/')
            })
            .catch((error) => {
                console.log(error)
            });
    }

    const handleGithubClick = () => {
        signInUserWithGithub()
            .then(() => {
                console.log('Login Successful')
                navigate(location?.state || '/')
            })
            .catch((error) => {
                console.log(error)
            });
    }

    return (
        <div className='min-h-[calc(100vh-148px)] flex flex-col gap-5 items-center justify-center bg-gray-300'>
            <h1>SignIn</h1>
            <form onSubmit={handleSignUp} className='flex flex-col gap-5'>
                <input type="text" name='name' className='input' placeholder='name' />
                <input type="url" name='url' className='input' placeholder='photoUrl' />
                <input type="email" name='email' className='input' placeholder='email' />
                <input type="password" name='password' className='input' placeholder='password' />
                <button className='btn' type='submit'>SignUp</button>
                <p>Already have an account, <Link to={"sign-in"} className='text-blue-400'>SignIn</Link></p>
                <hr />
                <button onClick={handleGoogleClick} className='btn btn-circle mx-auto'><FaGoogle></FaGoogle></button>
                <button onClick={handleGithubClick} className='btn btn-circle mx-auto'><FaGithub></FaGithub></button>
            </form>
        </div >
    );
};

export default SignUp;
```
