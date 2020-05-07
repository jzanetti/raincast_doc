Inputs for creating super ensemble
===================================

Configuration file
^^^^^^^^^^^^^^^^^^^

Super ensemble does not need a seperate configuration file, however the normal RainCast configuration file must be provided::

    sample_raincast_conf = get_configs.get_raincast_config(
        args.raincast_config_prefix + '_{}.yaml'.format(args.models[0]))

However, the normal RainCast configuration file must be adjusted, e.g., we only leave the probability and determinstic visualization on::

    enable_vis['postprocess']['allmembers'] = False
    enable_vis['postprocess']['probability'] = True
    enable_vis['postprocess']['determinstic'] = True
    enable_vis['postprocess']['model'] = False
    enable_vis['postprocess']['radar'] = False
    
    for key in enable_vis['debug']:
        enable_vis['debug'][key] = False


Weights for individual forecast
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The selected NWPs skills (with FSS) are calculated and normalized at the analysis time to determine the weights for different models. For example, we can get::

    {'nz4kmN-NCEP': 1.0, 'nz4kmN-ECMWF-SIGMA': 0.53, 'nz4kmN-UKMO': 0.59}

We also add the raw data as members of superensemble::

    # the raw model would take the half weights as its STEPS out
    cur_weight = int((weights_dict[cur_model]/2.0) * cur_steps_out.shape[0]) 
    cur_model_out = numpy.repeat(
        cur_model_out[numpy.newaxis, :, :, :], 
        cur_weight, axis=0)
