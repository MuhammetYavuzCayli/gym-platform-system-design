# Gym Platform System Design

A product and architecture case study for a fitness platform connecting individual users, personal trainers, gym coaches and gym owners.

The main challenge is not workout tracking.

It is designing flexible relationships between people and organizations.

> This repository demonstrates product architecture and domain modeling.  
> Production code and proprietary implementation details are intentionally excluded.

---

## Product Concept

The platform combines:

- Workout creation
- Exercise library
- Personal trainers
- Gyms
- Gym coaches
- Trainer discovery
- Followers
- Training programs
- Professional profiles

Users can create workouts while trainers and gyms can build professional relationships inside the platform.

---

## Roles

The system includes four main roles.

```text
Individual User

Personal Trainer

Gym Coach

Gym Owner
```

However, these roles are not completely independent.

A single person may participate in multiple contexts.

---

## Individual User

Individual users can:

- Browse exercises
- Create workouts
- Follow trainers
- Follow gyms
- Discover workout programs
- Save workout templates
- Track training activity

---

## Personal Trainer

A Personal Trainer operates independently.

They can:

- Build a professional profile
- Create workout templates
- Publish programs
- Gain followers
- Build reputation
- Apply to gyms
- Receive offers from gyms

A trainer remains an independent professional even when working with a gym.

---

## Gym Coach

A Gym Coach is not necessarily a separate permanent identity.

Instead, it can be represented as a relationship:

```text
Personal Trainer
      +
Gym Membership
      =
Gym Coach
```

This allows the trainer to remain independent while also working for a gym.

---

## Gym Owner

Gym Owners can:

- Create and manage gyms
- Manage gym profiles
- Invite trainers
- Accept trainer applications
- Create gym workout templates
- Manage active coaches
- End coach relationships

---

## Relationship Model

A key design decision is separating identity from relationships.

Instead of permanently changing:

```text
PersonalTrainer
→
GymCoach
```

the platform creates a relationship.

Example:

```text
Trainer
   ↓
GymTrainerRelationship
   ↓
Gym
```

The trainer remains a Personal Trainer.

---

## Relationship States

The relationship can have states such as:

```text
Pending
Active
Rejected
Terminated
```

Example:

```text
Personal Trainer
      ↓ Apply
Pending Relationship
      ↓ Accepted
Active Gym Coach
      ↓ Terminated
Personal Trainer
```

The trainer's independent profile remains active throughout the process.

---

## Invitation Flow

A Gym Owner can invite a trainer.

```text
Gym Owner
   ↓
Trainer Profile
   ↓
Send Invitation
   ↓
Trainer Reviews Offer
   ↓
Accept / Reject
```

If accepted:

```text
GymTrainerRelationship = Active
```

---

## Application Flow

The opposite direction is also possible.

```text
Trainer
   ↓
Gym Profile
   ↓
Apply to Gym
   ↓
Gym Reviews Application
   ↓
Accept / Reject
```

Both workflows create the same underlying relationship.

---

## Ending the Relationship

Either party may end the collaboration.

```text
Trainer
OR
Gym Owner
      ↓
Terminate Relationship
      ↓
Relationship = Terminated
```

The trainer then continues using the platform as an independent Personal Trainer.

---

## Professional History

Previous gym relationships can become part of the trainer's professional history.

Example:

```text
Experience

Gym A
Coach
2025 - 2026

Gym B
Coach
2024 - 2025
```

However, the trainer controls visibility.

```text
Public
Private
```

This allows users to build professional reputation without forcing all work history to become public.

---

## Follow System

Individual users can follow trainers.

```text
User
 ↓
Follow
 ↓
Trainer
```

This creates a reputation layer inside the platform.

A trainer profile can display:

```text
Followers
Published Programs
Professional Experience
Active Gym
Workout Templates
```

---

## Workout Builder

Users and trainers can create structured workouts.

Example:

```text
Workout:
HIIT Beginner

Exercise 1
Jumping Jacks
30 sec

Rest
30 sec

Exercise 2
Squats
30 sec

Rest
30 sec
```

---

## Exercise Model

Each exercise may contain:

```text
Name
Category
Target Muscles
Animation
Instructions
Difficulty
Equipment
```

Example categories:

```text
HIIT
Abs
Legs
Upper Body
Mobility
Cardio
```

---

## Program Templates

Trainers can create reusable program templates.

Example:

```text
4 Week Beginner Program

Week 1
 ├── Workout A
 ├── Workout B
 └── Workout C

Week 2
 ├── Workout A
 ├── Workout B
 └── Workout C
```

Gym owners can also create gym-level templates.

---

## Ownership

Programs should clearly identify ownership.

```text
Template Owner

Trainer
OR
Gym
```

This avoids ambiguity when trainers collaborate with gyms.

---

## Simplified Domain Model

```text
User
│
├── TrainerProfile
│
├── Followers
│
└── Workouts

Gym
│
├── GymOwner
├── Coaches
└── GymTemplates

Trainer
│
├── Programs
├── WorkoutTemplates
├── Followers
├── Experience
└── GymRelationships

GymTrainerRelationship
│
├── Gym
├── Trainer
├── Status
├── StartDate
└── EndDate
```

---

## Core Product Principle

One of the most important design decisions is:

> Roles should not unnecessarily lock users into permanent identities.

A trainer should be able to:

```text
Work independently

AND

Work for Gym A

AND

Later leave Gym A

AND

Join Gym B
```

without losing their professional profile or audience.

---

## Marketplace Potential

Once the relationship model exists, the platform can evolve into a marketplace.

Possible future features:

```text
Trainer discovery
Paid training programs
Online coaching
Gym memberships
Trainer ratings
Trainer bookings
Premium profiles
Program marketplace
```

---

## Architecture Considerations

The backend should separate:

```text
Identity
Authorization
Professional Profiles
Organization Membership
Content Ownership
Social Relationships
```

This prevents role logic from spreading across unrelated product areas.

---

## Product Lessons

This project demonstrates an important principle:

Complex applications often become easier when roles are modeled as relationships instead of permanent labels.

The user's identity stays stable.

Their relationships change.

This makes the system more flexible and much closer to how real professional relationships work.

---

## Topics

`Fitness Tech` `Marketplace` `System Design` `Product Architecture` `RBAC` `Social Platform` `Mobile App`

---

## Author

**Muhammet Yavuz ÇAYLI**

Full-Stack Software Engineer & Product Builder

Building SaaS, web and mobile products for real business problems.
