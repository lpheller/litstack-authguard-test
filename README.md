# Litstack setup with web guard

## Steps to reproduce
1. Setup and install Laravel and Litstack.
2. Change the guard in your `config/lit.php` to `web`.
3. If you don't have a user, create a new one (e.g. with tinker).
> You may now log in to your litstack backend with a user from the default laravel users table. But the permissions  entry in your top menu will still be missing and visiting  http://your.app/admin/permissions will result in an 401 Error though.
4. Update your user model to use the `Spatie\Permission\Traits\HasRoles` trait.
5. Update the `guard_name` in your `permissions` table:
```sql
update permissions set guard_name = 'web' where guard_name = 'lit'
```
6. Update the `guard_name` in your `roles` table:
```sql
update roles set guard_name = 'web' where guard_name = 'lit'
```
7. Update the existing entry in your `model_has_roles` table to fit your user model:
```sql
update model_has_roles set model_type = 'App\\Models\\User' where role_id = 1
```
8. Clear you caches. 
9. You should now be able to  visit http://your.app/admin/permissions
