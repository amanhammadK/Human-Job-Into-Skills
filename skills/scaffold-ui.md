# Skill: Scaffold UI Component

> **Description:** Instantly generate production-ready React components with Tailwind CSS, TypeScript interfaces, and accessibility features.
> **Outcome:** A complete `.tsx` file ready to drop into the project.
> **Measurable Value:** Reduces boilerplate coding time by ~15 minutes per component.

## Instructions

When the user asks to "scaffold a [Component Name]":

1.  **Analyze Requirements:**
    - Identify necessary props (e.g., `title`, `imageSrc`, `onClick`).
    - Determine responsive behavior (mobile vs desktop).
    - Identify accessibility roles (e.g., `button`, `article`, `aria-label`).

2.  **Generate Code:**
    - Usage: `React.FC<Props>`
    - Styling: Use Tailwind CSS utility classes.
    - Icons: Use `lucide-react` imports if icons are needed.

3.  **Strict Output Format:**
    - Start with imports.
    - Define `interface Props`.
    - Export the component as default.
    - **Do not** include explanation text unless requested. Just the code.

## Example Prompt
"Scaffold a UserCard component with avatar, name, bio, and a 'Follow' button."

## Example Output
```tsx
import React from 'react';
import { UserPlus } from 'lucide-react';

interface UserCardProps {
  avatarUrl: string;
  name: string;
  bio: string;
  onFollow: () => void;
  isFollowing?: boolean;
}

const UserCard: React.FC<UserCardProps> = ({ 
  avatarUrl, 
  name, 
  bio, 
  onFollow, 
  isFollowing = false 
}) => {
  return (
    <article className="max-w-sm rounded-lg border border-gray-200 bg-white p-6 shadow-sm hover:shadow-md transition-shadow">
      <div className="flex flex-col items-center">
        <img 
          src={avatarUrl} 
          alt={`${name}'s avatar`} 
          className="h-24 w-24 rounded-full object-cover ring-2 ring-gray-100 mb-4"
        />
        <h3 className="mb-1 text-xl font-semibold text-gray-900">{name}</h3>
        <p className="mb-6 text-center text-sm text-gray-500">{bio}</p>
        
        <button
          onClick={onFollow}
          className={`
            flex items-center gap-2 rounded-full px-6 py-2 text-sm font-medium transition-colors
            ${isFollowing 
              ? 'bg-gray-100 text-gray-900 hover:bg-gray-200' 
              : 'bg-blue-600 text-white hover:bg-blue-700'}
          `}
          aria-pressed={isFollowing}
        >
          <UserPlus size={16} />
          {isFollowing ? 'Following' : 'Follow'}
        </button>
      </div>
    </article>
  );
};

export default UserCard;
```
