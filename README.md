# Tutorial: Creating a TODO Task Management App with Laravel API Backend and React Native

### Introduction:
In this tutorial, we'll walk through the process of creating a TODO task management app using Laravel as the API backend server and React Native for the frontend. The app will allow users to create, view, update, and delete tasks.

### Question to Address:
How can we create a TODO task management app that utilizes Laravel as the backend API server and React Native for the frontend, allowing users to manage their tasks efficiently?

### Prerequisites:

### Before we begin, ensure you have the following installed:

<ol>
<li>Composer (for Laravel)</li>
<li>Node.js and npm (for React Native)</li>
<li>Laravel</li>
<li>React Native CLI</li>
<li>Expo CLI (optional, but recommended for React Native development)</li>
<li>Step 1: Set up Laravel Backend:</li>
</ol>

### Create a new Laravel project:

```
composer create-project --prefer-dist laravel/laravel todo-backend
```

### Navigate to the project directory:

```
cd todo-backend
```

- Set up the database configuration in .env file.
- Create a migration for tasks:

```
php artisan make:migration create_tasks_table
```

### Define the schema for tasks in the migration file.
(database/migrations/YYYY_MM_DD_create_tasks_table.php). 

```
Schema::create('tasks', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('description')->nullable();
    $table->timestamps();
});
```

### Run the migration to create the tasks table:

```
php artisan migrate
```

### Create a model for tasks:

```
php artisan make:model Task

```

### Define the Task model with the necessary attributes and relationships.
(app/Models/Task.php)

```
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Task extends Model
{
    use HasFactory;

    protected $fillable = ['title', 'description'];
}
```

Create a controller for tasks:

```
php artisan make:controller TaskController
```

### Implement CRUD methods (index, store, show, update, destroy) in the TaskController.

```
namespace App\Http\Controllers;

use App\Models\Task;
use Illuminate\Http\Request;

class TaskController extends Controller
{
    public function index()
    {
        return Task::all();
    }

    public function store(Request $request)
    {
        return Task::create($request->all());
    }

    public function show(Task $task)
    {
        return $task;
    }

    public function update(Request $request, Task $task)
    {
        $task->update($request->all());
        return $task;
    }

    public function destroy(Task $task)
    {
        $task->delete();
        return response()->json([], 204);
    }
}
```

### Step 2: Set up Laravel API Routes:

#### Define routes for tasks CRUD operations in routes/api.php:

```
use App\Http\Controllers\TaskController;

Route::get('/tasks', [TaskController::class, 'index']);
Route::post('/tasks', [TaskController::class, 'store']);
Route::get('/tasks/{task}', [TaskController::class, 'show']);
Route::put('/tasks/{task}', [TaskController::class, 'update']);
Route::delete('/tasks/{task}', [TaskController::class, 'destroy']);
```


#### Step 3: Set up React Native Frontend:

#### Create a new React Native project named TodoApp:

```
npx react-native init TodoApp
```

#### SIDE NOTE

  Run instructions for Android:
    • Have an Android emulator running (quickest way to get started), or a device connected.
    • cd "/Users/gyapom/Code/Laravel-ReactNative/laravel-reactnative-frontend/TodoApp" && npx react-native run-android
  
  Run instructions for iOS:
    • cd "/Users/gyapom/Code/Laravel-ReactNative/laravel-reactnative-frontend/TodoApp/ios"
    
    • Install Cocoapods
      • bundle install # you need to run this only once in your project.
      • bundle exec pod install
      • cd ..
    
    • npx react-native run-ios
    - or -
    • Open TodoApp/ios/TodoApp.xcodeproj in Xcode or run "xed -b ios"
    • Hit the Run button
    
  Run instructions for macOS:
    • See https://aka.ms/ReactNativeGuideMacOS for the latest up-to-date instructions.

#### Navigate to the project directory:

```
cd TodoApp
```

#### Install necessary dependencies:

```
npm install axios @react-navigation/native @react-navigation/stack react-native-gesture-handler react-native-reanimated

```

#### Link dependencies (if not linked automatically):

```
npx pod-install ios
```

#### Create screens and components for tasks (e.g., TaskListScreen.js, TaskDetailScreen.js, TaskFormScreen.js).

#### Implement navigation between screens using React Navigation.

#### Set up Axios for making HTTP requests to the Laravel API backend.

#### Implement functions for fetching tasks, creating tasks, updating tasks, and deleting tasks in React Native.


```
import axios from 'axios';

const BASE_URL = 'http://localhost:8000/api/tasks';

export const getTasks = async () => {
  try {
    const response = await axios.get(BASE_URL);
    return response.data;
  } catch (error) {
    console.error('Error fetching tasks:', error);
    return [];
  }
};

export const createTask = async (taskData) => {
  try {
    const response = await axios.post(BASE_URL, taskData);
    return response.data;
  } catch (error) {
    console.error('Error creating task:', error);
    throw error;
  }
};

export const updateTask = async (taskId, taskData) => {
  try {
    const response = await axios.put(`${BASE_URL}/${taskId}`, taskData);
    return response.data;
  } catch (error) {
    console.error('Error updating task:', error);
    throw error;
  }
};

export const deleteTask = async (taskId) => {
  try {
    await axios.delete(`${BASE_URL}/${taskId}`);
  } catch (error) {
    console.error('Error deleting task:', error);
    throw error;
  }
};
```

### Step 4: Connect React Native Frontend to Laravel Backend:

Ensure Laravel backend is running (use php artisan serve).

Update the base URL in React Native Axios configuration to point to your Laravel backend server.

Test API endpoints using tools like Postman to ensure they are accessible and functioning correctly.

Integrate API calls into React Native functions for CRUD operations on tasks.

### Step 5: Test and Debug:

Test the TODO app on both Android and iOS simulators/emulators as well as physical devices.

Debug any issues that arise during testing.

Ensure that data is being transmitted correctly between the React Native frontend and Laravel backend.

Handle errors gracefully and provide appropriate feedback to the user.

### Conclusion:
In this tutorial, we have created a TODO task management app using Laravel as the API backend server and React Native for the frontend. By following the steps outlined above, you should now have a functional app that allows users to manage their tasks efficiently. Happy coding!
















