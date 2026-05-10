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
  - [Example 1 with React:](#example-1-with-react)
  - [Example 2 with Next.js:](#example-2-with-nextjs)
    - [Next.js frontend:](#nextjs-frontend)
    - [Express server:](#express-server)


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

## Example 1 with React:

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


## Example 2 with Next.js:

https://github.com/tamim-111/firebase-auth-example-on-next.js
https://github.com/tamim-111/firebase-auth-example-on-express

### Next.js frontend:

```
NEXT_PUBLIC_FIREBASE_API_KEY=....
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=...
NEXT_PUBLIC_FIREBASE_PROJECT_ID=
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=
NEXT_PUBLIC_FIREBASE_APP_ID=
JWT_ACCESS_SECRET=48c7ae40080b52a273cd579da2df72099b6d2d1648279ea03b56f2e4b58dcbdc1ca0e6cde63d6771b9f6b11de9e6ccfce1ec1eef7e7c74c8bc02d8bbc15d52f0
# require('crypto').randomBytes(64).toString('hex')
NEXT_PUBLIC_API_URL=http://localhost:5000
```

```ts
// src/lib/firebase/firebase.init.ts

import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

const firebaseConfig = {
    apiKey: process.env.NEXT_PUBLIC_FIREBASE_API_KEY,
    authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
    projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
    storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
    messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
    appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
```

```tsx
// src/hooks/useAuth.ts

"use client";

import { AuthContext } from "@/contexts/AuthContext";
import { useContext } from "react";

export const useAuth = () => {
    const context = useContext(AuthContext);
    // const context = use(AuthContext);

    if (!context) {
        throw new Error("useAuth must be used inside AuthProvider");
    }

    return context;
};
```

```tsx
// src/contexts/authContext.ts
import { createContext, Dispatch, SetStateAction, } from "react";
import { User, UserCredential } from "firebase/auth";
import { UpdateUserData } from "@/providers/auth-provider";


export type AuthContextType = {
    user: User | null;
    loading: boolean;
    setUser: Dispatch<SetStateAction<User | null>>;

    signIn: (
        email: string,
        password: string
    ) => Promise<UserCredential>;

    signUp: (
        email: string,
        password: string
    ) => Promise<UserCredential>;

    googleLogin: () => Promise<UserCredential>;

    logout: () => Promise<void>;

    updateUserInfo: (
        updatedData: UpdateUserData
    ) => Promise<void>;
};

export const AuthContext = createContext<AuthContextType | null>(null);
```

```tsx
// src/providers/auth-provider.tsx
"use client";

import { AuthContext } from "@/contexts/AuthContext";
import { auth } from "@/lib/firebase/firebase.init";
import {
    GoogleAuthProvider, onAuthStateChanged, signInWithPopup,
    signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut,
    updateProfile, User,
} from "firebase/auth";
import { useEffect, useState, ReactNode, } from "react";

export type UpdateUserData = {
    displayName?: string | null;
    photoURL?: string | null;
};

const googleProvider = new GoogleAuthProvider();

export default function AuthProvider({ children }: { children: ReactNode }) {

    const [user, setUser] = useState<User | null>(null);
    const [loading, setLoading] = useState(true);


    const syncUserToDB = async (user: User) => {
        try {
            const idToken = await user.getIdToken();

            await fetch(`${process.env.NEXT_PUBLIC_API_URL}/users`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: `Bearer ${idToken}`,
                },
                credentials: "include",
                body: JSON.stringify({
                    name: user.displayName,
                    email: user.email,
                    photoURL: user.photoURL,
                }),
            });

        } catch (err) {
            console.error("User sync failed", err);
        }
    };

    // Email Login
    const signIn = async (email: string, password: string) => {
        setLoading(true);

        const result = await signInWithEmailAndPassword(auth, email, password);

        const idToken = await result.user.getIdToken();

        await fetch(`${process.env.NEXT_PUBLIC_API_URL}/jwt`, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${idToken}`,
            },
            credentials: "include",
            body: JSON.stringify({
                email: result.user.email,
            }),
        });

        setLoading(false);
        return result;
    };

    // Email Signup
    const signUp = async (email: string, password: string) => {
        setLoading(true);

        const result = await createUserWithEmailAndPassword(auth, email, password);

        const idToken = await result.user.getIdToken();

        await fetch(`${process.env.NEXT_PUBLIC_API_URL}/jwt`, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${idToken}`,
            },
            credentials: "include",
            body: JSON.stringify({
                email: result.user.email,
            }),
        });

        await syncUserToDB(result.user); // 🔥 moved here

        setLoading(false);
        return result;
    };

    // Google Login
    const googleLogin = async () => {
        setLoading(true);

        const result = await signInWithPopup(auth, googleProvider);

        const idToken = await result.user.getIdToken();

        await fetch(`${process.env.NEXT_PUBLIC_API_URL}/jwt`, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${idToken}`,
            },
            credentials: "include",
            body: JSON.stringify({
                email: result.user.email,
            }),
        });

        await syncUserToDB(result.user); // 🔥 moved here

        setLoading(false);
        return result;
    };

    // Logout
    const logout = async () => {
        await fetch(`${process.env.NEXT_PUBLIC_API_URL}/jwt-logout`, {
            method: "POST",
            credentials: "include",
        });

        await signOut(auth);
    };

    // Update Profile
    const updateUserInfo = async (updatedData: UpdateUserData) => {

        if (!auth.currentUser) {
            throw new Error(
                "No authenticated user found"
            );
        }

        return updateProfile(auth.currentUser, updatedData);
    };

    // Auth Observer
    useEffect(() => {
        const unsubscribe = onAuthStateChanged(auth, async (currentUser) => {
            setUser(currentUser);

            try {
                if (currentUser?.email) {

                    const idToken = await currentUser.getIdToken();

                    await fetch(`${process.env.NEXT_PUBLIC_API_URL}/jwt`, {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json",
                            Authorization: `Bearer ${idToken}`,
                        },
                        credentials: "include",
                        body: JSON.stringify({
                            email: currentUser.email,
                        }),
                    });
                }

            } catch (err) {
                console.error(err);
            } finally {
                setLoading(false);
            }
        });

        return () => unsubscribe();
    }, []);

    const authInfo = {
        user,
        setUser,
        loading,
        signIn,
        signUp,
        googleLogin,
        logout,
        updateUserInfo,
    };

    return (
        <AuthContext.Provider value={authInfo}>
            {children}
        </AuthContext.Provider>
    );
}
```



```tsx
// src/proxy.ts

import { NextRequest, NextResponse } from "next/server";

const sellerRoutes = [
    "/seller",
];

const adminRoutes = [
    "/admin",
];

function matchRoute(pathname: string, routes: string[]) {
    return routes.some((route) =>
        pathname.startsWith(route)
    );
}

export default async function proxy(req: NextRequest) {
    const { pathname } = req.nextUrl;
    const token = req.cookies.get("token")?.value;

    if (!token) {
        return NextResponse.redirect(
            new URL(`/sign-in?redirect=${pathname}`, req.url)
        );
    }

    try {
        const response = await fetch(
            `${process.env.NEXT_PUBLIC_API_URL}/users/me`,
            {
                headers: {
                    cookie: `token=${token}`,
                },
            }
        );

        if (!response.ok) {
            return NextResponse.redirect(
                new URL("/", req.url)
            );
        }

        const data = await response.json();
        const role = data?.result?.role;

        if (matchRoute(pathname, sellerRoutes)) {
            if (!["seller", "admin"].includes(role)) {
                return NextResponse.redirect(new URL("/forbidden", req.url));
            }
        }

        if (matchRoute(pathname, adminRoutes)) {
            if (role !== "admin") {
                return NextResponse.redirect(new URL("/forbidden", req.url));
            }
        }

        return NextResponse.next();

    } catch (error) {
        console.log(error);
        return NextResponse.redirect(new URL("/", req.url));
    }
}
export const config = {
    matcher: [

        /*
        Authenticated user routes
        */
        "/profile/:path*",

        /*
        Seller routes
        */
        "/seller/:path*",

        /*
        Admin routes
        */
        "/admin/:path*",
    ],
};
```

```tsx
// src/app/sign-up/page.tsx
"use client";

import { useAuth } from "@/hooks/useAuth";
import Link from "next/link";
import { useRouter, useSearchParams } from "next/navigation";
import { FaGoogle } from "react-icons/fa";

export default function SignUpPage() {
    const { signUp, googleLogin, updateUserInfo, loading } = useAuth();
    const router = useRouter();

    const searchParams = useSearchParams();
    const redirect = searchParams.get("redirect") || "/";

    const handleSignUp = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();

        const form = new FormData(e.currentTarget);

        const name = form.get("name") as string;
        const photoURL = form.get("photoURL") as string;
        const email = form.get("email") as string;
        const password = form.get("password") as string;

        try {
            await signUp(email, password);

            await updateUserInfo({
                displayName: name,
                photoURL,
            });


            router.push(redirect);
        } catch (err) {
            console.error(err);
        }
    };

    const handleGoogle = async () => {
        try {
            await googleLogin();
            router.push(redirect);
        } catch (err) {
            console.error(err);
        }
    };

    return (
        <div className="flex flex-col items-center justify-center gap-5">
            <h1 className="text-2xl font-bold">Sign Up</h1>

            <form onSubmit={handleSignUp} className="flex flex-col gap-4">
                <input name="name" type="text" placeholder="name" className="input" />
                <input name="photoURL" type="url" placeholder="photo url" className="input" />
                <input name="email" type="email" placeholder="email" className="input" />
                <input name="password" type="password" placeholder="password" className="input" />

                <button disabled={loading} className="btn">
                    Sign Up
                </button>

                <p>
                    Already have account?{" "}
                    <Link href="/sign-in" className="text-blue-500">
                        Sign in
                    </Link>
                </p>

                <button type="button" onClick={handleGoogle} className="btn btn-circle">
                    <FaGoogle />
                </button>
            </form>
        </div>
    );
}
```


```tsx
// src/app/sign-in/page.tsx
"use client";

import { useAuth } from "@/hooks/useAuth";
import Link from "next/link";
import { useRouter, useSearchParams } from "next/navigation";
import { FaGoogle } from "react-icons/fa";

export default function SignInPage() {
    const { signIn, googleLogin, loading } = useAuth();
    const router = useRouter();
    const searchParams = useSearchParams();

    const redirect = searchParams.get("redirect") || "/";

    const handleSignIn = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();

        const form = new FormData(e.currentTarget);

        const email = form.get("email") as string;
        const password = form.get("password") as string;

        try {
            await signIn(email, password);
            router.push(redirect);
        } catch (err) {
            console.error(err);
        }
    };

    const handleGoogle = async () => {
        try {
            await googleLogin();
            router.push(redirect);
        } catch (err) {
            console.error(err);
        }
    };

    return (
        <div className="flex flex-col items-center justify-center gap-5">
            <h1 className="text-2xl font-bold">Sign In</h1>

            <form onSubmit={handleSignIn} className="flex flex-col gap-4">
                <input name="email" type="email" placeholder="email" className="input" />
                <input name="password" type="password" placeholder="password" className="input" />

                <button disabled={loading} className="btn">
                    Sign In
                </button>

                <p>
                    No account? <Link href="/sign-up" className="text-blue-500">Sign up</Link>
                </p>

                <button type="button" onClick={handleGoogle} className="btn btn-circle">
                    <FaGoogle />
                </button>
            </form>
        </div>
    );
}
```

```tsx
// src/components/Navbar.tsx

"use client"

import { useAuth } from '@/hooks/useAuth';
import Image from 'next/image'
import Link from 'next/link'

export default function Navbar() {

    const { user, logout } = useAuth();

    const handleLogOut = async () => {
        try {
            await logout();
            alert("Sign out successful");
        } catch (err) {
            console.error(err);
            alert("Sign out failed");
        }
    };

    return (
        <div className='flex justify-end items-center gap-3 p-2 border mb-5'>
            <Link href={'/'}>Home</Link>
            <Link href={'/profile'}>Profile</Link>
            <Link href={'/seller'}>Seller</Link>
            <Link href={'/admin'}>Admin</Link>
            {
                !user
                    ?
                    <>
                        <Link href={'/sign-in'}>Sign In</Link>
                        <Link href={'/sign-up'}>Sign Up</Link>
                    </>
                    :
                    <>
                        <Image src={user?.photoURL || ''} alt='logo' width={25} height={25} className='rounded-full'></Image>
                        <button onClick={handleLogOut} className='btn btn-error btn-sm'>Sign Out</button>
                    </>
            }

        </div>
    )
}
```

### Express server:

```js
// index.js

const express = require("express");
const cors = require("cors");
require("dotenv").config();
const { MongoClient, ServerApiVersion, ObjectId, } = require("mongodb");
const jwt = require("jsonwebtoken");
const cookieParser = require("cookie-parser");
const admin = require("./firebase-admin");
const app = express();
const port = process.env.PORT || 5000;
app.use(cors({
    origin: ["http://localhost:3000", "add others url here"],
    credentials: true,
})
);
app.use(express.json());
app.use(cookieParser());


const client = new MongoClient(process.env.MONGODB_URI, {
    serverApi: {
        version: ServerApiVersion.v1,
        strict: true,
        deprecationErrors: true,
    },
});

const usersCollection = client.db("usersDB").collection("users");

const verifyProviderUser = async (req, res, next) => {

    try {
        const authHeader = req.headers.authorization;

        if (!authHeader?.startsWith("Bearer ")) {

            return res.status(401).send({
                success: false,
                message: "Unauthorized",
            });
        }

        const providerToken = authHeader.split(" ")[1];

        // HERE: verify firebase/clerk/authjs token
        const decoded = await admin.auth().verifyIdToken(providerToken);
        req.firebaseUser = decoded;

        next();

    } catch {

        return res.status(401).send({
            success: false,
            message: "Invalid provider token",
        });
    }
};

const verifyJwt = async (req, res, next) => {
    try {
        const token = req?.cookies?.token;

        if (!token) {
            return res.status(401).send({
                success: false,
                message: "Access token missing",
            });
        }

        const decoded = jwt.verify(token, process.env.JWT_ACCESS_SECRET);

        req.auth = decoded;

        next();
    } catch (error) {
        return res.status(401).send({
            success: false,
            message: "Authentication failed",
        });
    }
};

const verifyRole = (...roles) => {
    return async (req, res, next) => {
        try {
            if (!req.auth?.email) {
                return res.status(401).send({
                    success: false,
                    message: "Authentication required",
                });
            }

            const dbUser = await usersCollection.findOne({ email: req.auth.email, });

            if (!dbUser) {
                return res.status(404).send({
                    success: false,
                    message: "User not found",
                });
            }

            if (!roles.includes(dbUser.role)) {
                return res.status(403).send({
                    success: false,
                    message: `Access denied. Required role: ${roles.join(", ")}`,
                });
            }

            /*
            attach latest DB user
            */
            req.user = dbUser;

            next();
        } catch (error) {
            return res.status(500).send({
                success: false,
                message: "Role verification failed",
            });
        }
    };
};

async function run() {
    try {

        await client.connect();

        await client.db("admin").command({ ping: 1 });

        console.log(
            "MongoDB connected successfully"
        );

        app.post("/jwt", verifyProviderUser, async (req, res) => {
            try {
                // const { email } = req.body; // if we don't want to use firebase
                const email = req.firebaseUser.email;

                if (!email) {
                    return res.status(400).send({
                        success: false,
                        message: "Email is required",
                    });
                }

                /*
                find user from database
                */
                const user = await usersCollection.findOne({ email, });

                if (!user) {
                    return res.status(404).send({
                        success: false,
                        message: "User not found",
                    });
                }

                const jwtPayload = {
                    id: user._id.toString(),
                    email: user.email,
                };

                const token = jwt.sign(jwtPayload, process.env.JWT_ACCESS_SECRET, { expiresIn: "7d", });

                res.cookie("token", token, {
                    httpOnly: true,
                    secure: false, // production: true
                    sameSite: "lax", // production: "none"
                });

                return res.send({
                    success: true,
                    message: "Authentication successful",
                });
            } catch (error) {
                return res.status(500).send({
                    success: false,
                    message: "JWT generation failed",
                });
            }
        });


        app.post("/jwt-logout", (req, res) => {
            res.clearCookie("token", {
                httpOnly: true,
                secure: false,
                sameSite: "lax",
            });

            res.send({
                success: true,
                message: "User logged out successfully",
            });
        });

        /*
        create/sync user
        */
        app.post("/users", verifyProviderUser, async (req, res) => {
            try {
                const user = req.body;
                const firebaseEmail = req.firebaseUser.email;

                if (!firebaseEmail) {
                    return res.status(400).send({
                        success: false,
                        message: "Email is required",
                    });
                }

                const filter = { email: firebaseEmail, };

                const updateDoc = {
                    $setOnInsert: {
                        name: user.name,
                        email: firebaseEmail,
                        photoURL: user.photoURL,
                        role: "user",
                        createdAt: new Date(),
                    },
                };

                const options = {
                    upsert: true,
                };

                const result = await usersCollection.updateOne(filter, updateDoc, options);

                return res.send({
                    success: true,
                    message: "User synced successfully",
                    result,
                });
            } catch (error) {
                return res.status(500).send({
                    success: false,
                    message: "Failed to sync user",
                });
            }
        });

        /*
        get current user
        */
        app.get("/users/me", verifyJwt, async (req, res) => {
            try {
                const user = await usersCollection.findOne({ email: req.auth.email, });

                if (!user) {
                    return res.status(404).send({
                        success: false,
                        message: "User not found",
                    });
                }

                return res.send({
                    success: true,
                    result: user,
                });
            } catch (error) {
                return res.status(500).send({
                    success: false,
                    message: "Failed to get user",
                });
            }
        });


        app.get("/user-route", verifyJwt, async (req, res) => {
            res.send({
                success: true,
                message: "Protected user route",
            });
        });


        app.get("/seller-route", verifyJwt, verifyRole("seller"), async (req, res) => {
            res.send({
                success: true,
                message: "Seller route access granted",
            });
        }
        );


        app.get("/admin-route", verifyJwt, verifyRole("admin"), async (req, res) => {
            res.send({
                success: true,
                message: "Admin route access granted",
            });
        }
        );

        app.get("/seller-admin-route", verifyJwt, verifyRole("seller", "admin"), async (req, res) => {
            res.send({
                success: true,
                message: "Seller and Admin route access granted",
            });
        }
        );


        //  Update User Role (Admin Only)
        app.patch("/users/role/:id", verifyJwt, verifyRole("admin"), async (req, res) => {
            try {
                const id = req.params.id;

                const { role } = req.body;

                const allowedRoles = [
                    "user",
                    "seller",
                    "admin",
                ];

                if (!allowedRoles.includes(role)) {
                    return res.status(400).send({
                        success: false,
                        message: "Invalid role",
                    });
                }

                const updateDoc = {
                    $set: {
                        role,
                    },
                }

                const result = await usersCollection.updateOne({ _id: new ObjectId(id), }, updateDoc);

                return res.send({
                    success: true,
                    message: "User role updated successfully",
                    result,
                });
            } catch (error) {
                return res.status(500).send({
                    success: false,
                    message: "Failed to update role",
                });
            }
        }
        );

    } catch (error) {
        console.error(error);
    }
}

run().catch(console.dir);


app.get("/", (req, res) => {
    res.send("Server is running");
});


app.listen(port, () => {
    console.log(`Server running on port ${port}`);
});
```

```js
// firebase-admin.js

const admin = require("firebase-admin");

if (!admin.apps.length) {

    admin.initializeApp({
        credential: admin.credential.cert({
            projectId: process.env.FIREBASE_PROJECT_ID,
            clientEmail: process.env.FIREBASE_CLIENT_EMAIL,

            privateKey: process.env.FIREBASE_PRIVATE_KEY.replace(/\\n/g, "\n"),
        }),
    });
}

module.exports = admin;
```

```js
# .env
MONGODB_URI=mongodb://localhost:27017/
PORT = 5000
JWT_ACCESS_SECRET=48c7ae40080b52a273cd579da2df72099b6d2d1648279ea03b56f2e4b58dcbdc1ca0e6cde63d6771b9f6b11de9e6ccfce1ec1eef7e7c74c8bc02d8bbc15d52f0
# require('crypto').randomBytes(64).toString('hex')

FIREBASE_PROJECT_ID=...
FIREBASE_CLIENT_EMAIL=....
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----END PRIVATE KEY-----\n"
```


