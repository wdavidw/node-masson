
# FSTAB

This module handles fstab and mountpoints.

    module.exports = ->
      'check':
        'masson/core/fstab/check'
      'configure':
        'masson/core/fstab/configure'
      'install': [
        'masson/core/fstab/install'
        'masson/core/fstab/check'
      ]