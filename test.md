---
layout: page
title: Test
permalink: /test/
---

# Test

## This is a test

Here's a sample code snippet

```javascript
let x = 2;
let y = "Number two: ";

console.log(y + x);
```


## C#

```c#
using DTID.BusinessLogic.Models;
using DTID.Data;
using DTID.BusinessLogic.ViewModels.RoleViewModel;

namespace DTID.Controllers
{
    [Produces("application/json")]
    [Route("api/PermissionRoles")]
    public class PermissionRolesController : Controller
    {
        private readonly ApplicationDbContext _context;

        public PermissionRolesController(ApplicationDbContext context)
        {
            _context = context;
        }

        // GET: api/PermissionRoles
        [HttpGet]
        public IEnumerable<PermissionRole> GetPermissionRole()
        {
            return _context.PermissionRole;
        }

        [HttpGet("getPermission/{id}")]
        public IEnumerable<PermissionRole> GetPermissions([FromRoute] int id)
        {
            var user = _context.Users.Find(id);
            if (user == null)
                return new List<PermissionRole>();
            return _context.PermissionRole.Include(permission => permission.Permission)
                .Where(role => role.RoleID == user.RoleID).Where(pr => pr.IsEnabled).ToList();
        }
```