<div class="dashboard">
  <header class="header">
    <h1>{{ title() }}</h1>
    <button (click)="toggleForm()" class="btn-primary">
      @if (showForm()) {
        Cancel
      } @else {
        Add New User
      }
    </button>
  </header>

  @if (showForm()) {
    <div class="form-container">
      <form [formGroup]="form" (ngSubmit)="onSubmit()">
        <div class="form-group">
          <label for="name">Name</label>
          <input
            type="text"
            id="name"
            formControlName="name"
            placeholder="Enter user name"
            class="form-input"
          />
          @if (form.get('name')?.invalid && form.get('name')?.touched) {
            <span class="error">Name must be at least 3 characters</span>
          }
        </div>

        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            formControlName="email"
            placeholder="Enter email address"
            class="form-input"
          />
          @if (form.get('email')?.invalid && form.get('email')?.touched) {
            <span class="error">Please enter a valid email</span>
          }
        </div>

        <div class="form-group">
          <label for="phone">Phone Number</label>
          <input
            type="text"
            id="phone"
            formControlName="phone"
            placeholder="Enter 11-digit phone number"
            class="form-input"
          />
          @if (form.get('phone')?.invalid && form.get('phone')?.touched) {
            <span class="error">Please enter a valid 10-digit phone number</span>
          }
        </div>

        <div class="form-group">
          <label for="age">Age</label>
          <input
            type="number"
            id="age"
            formControlName="age"
            placeholder="Enter age (18-80)"
            class="form-input"
          />
          @if (form.get('age')?.invalid && form.get('age')?.touched) {
            <span class="error">Age must be between 18 and 80</span>
          }
        </div>

        <div class="form-actions">
          <button type="submit" [disabled]="form.invalid" class="btn-primary">
            Add User
          </button>
          <button type="button" (click)="toggleForm()" class="btn-secondary">
            Cancel
          </button>
        </div>
      </form>
    </div>
  }

  <div class="table-container">
    <table class="users-table" role="table" aria-label="List of users">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Age</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        @for (user of users(); track user.id) {
          <tr class="table-row">
            <td class="table-cell">{{ user.id }}</td>
            <td class="table-cell">{{ user.name }}</td>
            <td class="table-cell">{{ user.email }}</td>
            <td class="table-cell">{{ user.phone }}</td>
            <td class="table-cell">{{ user.age }}</td>
            <td class="table-cell">
              <button
                (click)="deleteUser(user.id)"
                class="btn-delete"
                aria-label="Click to delete this user"
              >
                Delete
              </button>
            </td>
          </tr>
        } @empty {
          <tr>
            <td colspan="6" class="empty-state">No users found. Click the button above to add a new user.</td>
          </tr>
        }
      </tbody>
    </table>
  </div>
</div>

<router-outlet></router-outlet>
