Identified Issues
======================

Introduction
------------

In an effort to determine the quality of the original project, issues are listed below. In the code there is a
tag for each Identified issue which has the following format:

.. code-block:: javascript

    // Identified Issue: <Issue Number>

The issue number is a unique identifier for the issue.

Identified Issue: 0
-------------------

The current code lacks proper password checking logic. It appears that passwords are stored in the database in
both plain text and hashed form. However, the code sets a variable called 'checkPassword' to 'true,' indicating
that passwords are always considered correct. This is a security vulnerability as it does not verify passwords
against their hashed counterparts.

Identified Issue: 1
-------------------

Missing a way to load various profile information that is expected to be loaded on the main page.
This includes Total badges earned, linkedIn profile, etc.

After looking through the current software, there doesn't appear to be a way to set the LinkedIn information.

**Server side handling**

genics-app/pages/api/students/[id].js is a dynamic route that allows for retrieving a student's information.
During runtime, id is set to the user id of the student. The code then queries the database for the student's
information

For example, if the user id is **as213as21** then the path will look like this:
genics-app/pages/api/students/**as213as21**.js

This is done through an HTTP GET request. 

.. code-block:: javascript
    :emphasize-lines: 3

      switch (method) {
        case "GET":
        await getStudent(req, res);
        break;

        case "PATCH":
        await updateStudent(req, res);
        break;

        case "DELETE":
        await deleteStudent(req, res);
        break;

        default:
        throw new Error(
            `The HTTP ${method} method is not supported at this route.`
        );
        break;
    }

This code will query the students collection in the database using the id. Upon finding the student
information, it will return the information in JSON format. the `res` object is used to send the
response back to the client.

.. code-block:: javascript
    :emphasize-lines: 11

    const getStudent = async (req, res) => {

    try {
        const student = await Student.findOne({
        // student: req.student,
        _id: req.query.id,
        });

        res.status(200).json({
        status: "success",
        data: student,
        });
    } catch (error) {
        res.send(error);
    }
    };

**Client Handling**

genics-app/components/users/student/student-profile.js is the module that handles the client side of the
student profile.

Upon loading the page, the client will make a GET request to the server to retrieve the student's information.

.. code-block:: javascript
    :emphasize-lines: 4

    const getUser = useCallback(async () => {

      if (session) {
        setUser(await getStudentProfile())
      } 
    }, [session]);


Note that the setUser function is a React component that allows updates to variables without having to reload the page.
**setUser** will set the variable called *user*. The below code is how you register this kind of variables.

The format is as follows: 
    const [<variable-name>, <function-name>] = useState([<initial-value>]);

Here is the code for setUser:

.. code-block:: javascript

    const [user, setUser] = useState([]);

**getStudentProfile**:

.. code-block:: javascript
    :emphasize-lines: 7

    const getStudentProfile = async () => {
      if (session) {
        const res = await fetch("/api/students/" + session.user.id, {
            method: "GET",
          });
          const data = await res.json()
          return data;
      }
    };

**Showing the information to the user**

The highlighted line below expects *user?.data?.linkedIn?user.data.linkedIn*
to be an existing object, and if it isnt, it will simply use an empty string.

.. code-block:: html
    :emphasize-lines: 5

    <div className='h-full'>
    <StudentInfo 
        name={user?.data?.firstName?user.data.firstName:""}
        status={'online'}
        linkedIn={user?.data?.linkedIn?user.data.linkedIn:""}
        startDate={user?.data?.signupDate?user.data.signupDate:""}
        badgeCount={user?.data?.badgesEarned?user.data.badgesEarned.length:""}/>
    </div>
