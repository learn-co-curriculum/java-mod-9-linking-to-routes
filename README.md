# Linking to Routes

## Learning Goals

- Link to routes in Angular.

## Introduction

So far, we have to manually enter URLs in the browser's address bar to go to
each route. This a) really defeats the purpose of a SPA because the entire
application has to be reloaded every time and b) is not a convenient way for the
user to navigate the application anyway.

## Route Linking

In order to ask the router module to activate a specific route in the
application, we can use the `routerLink` directive on an HTML element. For
example, we will add the `routerLink` directive to the "New Message" `button`
element in the conversation control component:

```html
<div class="container">
  <div class="row">
    <div class="col-9">
      <div class="dropdown">
        <button
          class="btn btn-primary dropdown-toggle"
          type="button"
          data-bs-toggle="dropdown"
          aria-expanded="false"
        >
          Conversation
        </button>
        <ul class="dropdown-menu">
          <li *ngFor="let conversation of conversations">
            <a class="dropdown-item" href="#">
              <span
                *ngFor="let user of conversation.users; 
                                    let isLastConversation = last"
              >
                {{ user.firstName }}
                <span *ngIf="!isLastConversation">, </span>
              </span>
            </a>
          </li>
        </ul>
      </div>
    </div>
    <div class="col-3">
      <div class="float-end">
        <button class="btn btn-primary" [routerLink]="['/contactList']">
          <!-- adding the routerLink directive here -->
          New Message
        </button>
      </div>
    </div>
  </div>
</div>
```

The `routerLink` directive follows this syntax:

1. `[routerLink]="[<array of route elements]"`
2. The array of route elements are the various components of a route. Our routes
   in this application only one component, but imagine a route to load a
   specific conversation might look like this:
   `http://localhost:4200/conversations/1`, where "1" is the conversation Id. In
   that case, the route element array would have 2 entries

Let's make a similar change to the contact list in
`contact-list-component.component.html` view to let it link back to the default
view:

```html
<div class="container">
  <div class="row">
    <div class="col-12">
      <h3>Contact List</h3>
    </div>
  </div>
  <div class="row" *ngFor="let user of users">
    <div class="col-12 border p-3">
      <app-contact-component [user]="user"></app-contact-component>
    </div>
  </div>

  <div class="row">
    <div class="col-9"></div>
    <div class="col-3 p-3">
      <div class="float-end">
        <button class="btn btn-primary" [routerLink]="['/']">
          <!-- adding the routerLink directive here -->
          Start Message
        </button>
      </div>
    </div>
  </div>
</div>
```

With that, you can now navigate to and from the contact list view in the
application. As you do that, you will notice that the entire application doesn't
reload, just the area where you have targeted the `router-outlet`. Angular's
router module does, however, take care of updating the browser's URL bar when a
specific route is activated, so the user can get a sense of where they are in
the application, and even bookmark a specific area of the application.
